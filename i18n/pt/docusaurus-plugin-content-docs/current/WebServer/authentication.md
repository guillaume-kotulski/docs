---
id: authentication
title: Autenticação
---

A autenticação de usuários é necessária quando se deseja fornecer direitos de acesso específicos aos usuários Web. A autenticação determina como as informações referentes às credenciais do usuário (geralmente nome e senha) são coletadas e processadas.

## Modos de autenticação

El servidor web 4D ofrece tres modos de autenticación, que puede seleccionar en la página **Web**/**Opciones (I)** de la ventana Propiedades:

![](../assets/en/WebServer/authentication.png)

> Se recomienda utilizar una autenticación **personalizada**.

### Visão Geral

O funcionamento do sistema de acesso do servidor web 4D está resumido no diagrama seguinte:

![](../assets/en/WebServer/serverAccess.png)

> Las peticiones que comienzan por `rest/` son gestionadas directamente por el [servidor REST](REST/configuration.md).

### Personalizado (padrão)

Basicamente, nesse modo, cabe ao desenvolvedor definir como autenticar os usuários. 4D sólo evalúa las peticiones HTTP [que requieren una autenticación](#database-method-calls).

Este modo de autenticação é o mais flexível porque permite que você:

- ou delegar a autenticação do usuário a um aplicativo de terceiros (por exemplo, uma rede social, SSO);
- o bien, ofrecer una interfaz al usuario (por ejemplo, un formulario web) para que pueda crear su cuenta en su base de datos clientes; luego, puede autenticar a los usuarios con cualquier algoritmo personalizado (ver [este ejemplo](sessions.md#example) del O importante é que você nunca armazene a senha de forma não protegida, usando esse código: O importante é que você nunca armazene a senha de forma não protegida, usando esse código: O importante é que você nunca armazene a senha de forma não protegida, usando esse código:

```4d
//... criar conta de usuário
ds.webUser.password:=Generate password hash($password)  
ds.webUser.save()
```

Ver también [este ejemplo](gettingStarted.md#authenticating-users) del capítulo "Cómo comenzar".

Se nenhuma autenticação personalizada for fornecida, 4D chama o método banco de dados [`On Web Authentication`](#on-web-authentication) (se existir). In addition to $urll and $content, only the IP addresses of the browser and the server ($IPClient and $IPServer) are provided, the user name and password ($user and $password) are empty. El método debe devolver **True** en $0 si el usuario se autentifica con éxito, entonces se sirve el recurso solicitado, o **False** en $0 si la autenticación falló.

> **Atención**: si el método de base de datos `On Web Authentication` no existe, las conexiones se aceptan automáticamente (modo de prueba).

### Protocolo Basic

Quando um usuário se conecta ao servidor, uma caixa de diálogo padrão é exibida no navegador para que ele digite o nome de usuário e a senha.

> O nome e a palavra-passe introduzidos pelo utilizador são enviados sem encriptação no cabeçalho do pedido HTTP. Este modo requer normalmente HTTPS para garantir a confidencialidade.

Os valores introduzidos são então avaliados:

- Si la opción **Incluir contraseñas de 4D** está marcada, las credenciales de los usuarios se evaluarán primero contra la [tabla interna de usuarios 4D](Users/overview.md).
  - Se o nome de usuário enviado pelo navegador existir na tabela de usuários 4D e a senha estiver correta, a conexão será aceita. Se a palavra-passe estiver incorreta, a ligação é recusada.
  - Se o nome de usuário não existir na tabela de usuários 4D, o método de banco de dados [`On Web Authentication`](#on-web-authentication) será chamado. Si el método base `On Web Authentication` no existe, se rechazan las conexiones.
- If the **Include 4D passwords** option is not checked, user credentials are sent to the [`On Web Authentication`](#on-web-authentication) database method along with the other connection parameters (IP address and port, URL...) para que você possa processá-los. Si el método base `On Web Authentication` no existe, se rechazan las conexiones.

> Com o servidor da Web 4D Client, lembre-se de que todos os sites publicados pelas máquinas 4D Client compartilharão a mesma tabela de usuários. Validação de usuários/senhas é realizada pela aplicação 4D Server.

### Protocolo DIGEST

Esse modo oferece um nível maior de segurança, pois as informações de autenticação são processadas por um processo unidirecional chamado hashing, que impossibilita decifrar seu conteúdo.

Como no modo BASIC, os usuários devem digitar seu nome e senha ao se conectarem. O método banco de dados [`On Web Authentication`](#on-web-authentication) é então chamado. Quando o modo DIGEST é ativado, o parâmetro $password (senha) é sempre retornado vazio. De fato, ao usar esse modo, essas informações não passam pela rede como texto claro (não criptografado). Por lo tanto, en este caso es imprescindible evaluar las solicitudes de conexión mediante el comando `WEB Validate digest`.

> Você deve reiniciar o servidor Web para que as alterações feitas nesses parâmetros sejam levadas em conta.

## On Web Authentication

El método de base de datos `On Web Authentication` se encarga de gestionar el acceso al motor del servidor web. É chamado por 4D ou 4D Server quando uma solicitação HTTP dinâmica é recebida.

### Chamadas dos métodos banco

El método base `On Web Authentication` se llama automáticamente cuando una solicitud o procesamiento requiere la ejecución de algún código 4D (excepto para las llamadas REST). Ele também é chamado quando o servidor Web recebe um URL estático inválido (por exemplo, se a página estática solicitada não existir).

Por tanto, se llama al método base `On Web Authentication`:

- quando o servidor da Web recebe um URL solicitando um recurso que não existe
- cuando el servidor web recibe una URL que empieza por `4DACTION/`, `4DCGI/`...
- when the web server receives a root access URL and no home page has been set in the Settings or by means of the [`WEB SET HOME PAGE`](../commands-legacy/web-set-home-page.md) command
- cuando el servidor web procesa una etiqueta que ejecuta código (por ejemplo, `4DSCRIPT`) en una página semidinámica.

Por tanto, NO se llama al método base `On Web Authentication`:

- quando o servidor Web recebe um URL solicitando uma página estática válida.
- when the web server receives a URL beginning with `rest/` and the REST server is launched (in this case, the authentication is handled through the [`ds.authentify` function](../REST/authUsers#force-login-mode) or (deprecated) the `On REST Authentication` database method or Structure settings.
- when the web server receives a URL with a pattern triggering a [custom HTTP Request Handler](http-request-handler.md).

### Sintaxe

**On Web Authentication**( *$url* : Text ; *$content* : Text ; *$IPClient* : Text ; *$IPServer* : Text ; *$user* : Text ; *$password* : Text ) -> $accept : Boolean

| Parâmetros | Tipo       |                             | Descrição                                                                |
| ---------- | ---------- | :-------------------------: | ------------------------------------------------------------------------ |
| $url       | Text       | <- | URL                                                                      |
| $content   | Text       | <- | Cabeçalhos HTTP + corpo HTTP (até um limite de 32 kb) |
| $IPClient  | Text       | <- | Endereço IP do cliente Web (browser)                  |
| $IPServer  | Text       | <- | Endereço IP do servidor                                                  |
| $user      | Text       | <- | Nome de usuario                                                          |
| $password  | Text       | <- | Senha                                                                    |
| $accept    | Parâmetros |              ->             | True = pedido aceite, False = pedido rejeitado                           |

Estes parâmetros devem ser declarados da seguinte forma:

```4d
// On Web Authentication database method
#DECLARE ($url : Text; $content : Text; \
  $IPClient : Text; $IPServer : Text; \
  $user : Text; $password : Text) \
  -> $accept : Boolean

//Code for the method

```

:::note

Todos los parámetros del método base `On Web Authentication` no están necesariamente rellenados. La información recibida por el método base depende del [modo de autenticación](#authentication-modes) seleccionado).

:::

#### $url - URL

O primeiro parâmetro (`$url`) é o URL recebido pelo servidor, do qual o endereço do host foi removido.

Vejamos o exemplo de uma ligação Intranet. Suponha que o endereço IP do seu Web Server 4D é 123.45.67.89. A tabela a seguir mostra os valores de $urll dependendo do URL inserida no navegador Web:

| URL introduzido no navegador Web                                                                                                                  | Valor do parâmetro $urll                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 123.45.67.89                                                                                      | /                                                                                     |
| http://123.45.67.89                                                               | /                                                                                     |
| 123.45.67.89/Customers                                                                            | /Customers                                                                            |
| http://123.45.67.89/Customers/Add                                                 | /Customers/Add                                                                        |
| 123.45.67.89/Do_This/If_OK/Do_That | /Do_This/If_OK/Do_That |

#### $content - Header and Body of the HTTP request

The second parameter (`$content`) is the header and the body of the HTTP request sent by the web browser. Tenga en cuenta que esta información se pasa a su método base `On Web Authentication` tal cual. Seu conteúdo varia conforme a natureza do navegador Web que está tentando se conectar.

Se o seu aplicativo usar essas informações, caberá a você analisar o cabeçalho e o corpo. Puede utilizar los comandos `WEB GET HTTP HEADER` y `WEB GET HTTP BODY`.

> For performance reasons, the size of data passing through the $content parameter must not exceed 32 KB. Para além deste tamanho, são truncados pelo servidor HTTP 4D.

#### $IPClient - Endereço IP do cliente Web

O parâmetro `$IPClient` recebe o endereço IP da máquina do navegador. Essas informações permitem distinguir entre conexões de intranet e de Internet.

> 4D devolve endereços IPv4 em formato híbrido IPv6/IPv4 escritos com um prefixo de 96 bits, por exemplo ::ffff:192.168.2.34 para o endereço IPv4 192.168.2.34. Para más información, consulte la sección [Soporte IPv6](webServerConfig.md#about-ipv6-support).

#### $IPServer - Endereço IP do servidor

El parámetro `$IPServer` recibe la dirección IP utilizada para llamar al servidor web. 4D permite multi-home que você explore máquinas com mais de um endereço IP. Para más información, consulte la [página Configuración](webServerConfig.md#ip-address-to-listen).

#### $user e $password - Nome de usuário e senha

The `$user` and `$password` parameters receive the user name and password entered by the user in the standard identification dialog box displayed by the browser. Esta caja de diálogo aparece para cada conexión, si se selecciona la autenticación [basic](#basic-protocol) o [digest](#digest-protocol).

> If the user name sent by the browser exists in 4D, the $password parameter (the user’s password) is not returned for security reasons.

#### $accept - Retorno de função

The `On Web Authentication` database method returns a boolean:

- If it is True, the connection is accepted.

- If it is False, the connection is refused.

El método base `On Web Connection` sólo se ejecuta si la conexión ha sido aceptada por `On Web Authentication`.

:::warning

- If no value is returned, the connection is considered as **accepted** and the `On Web Connection` database method is executed.
- Do not call any interface elements in the `On Web Authentication` database method (`ALERT`, `DIALOG`, etc.) because otherwise its execution will be interrupted and the connection refused. O mesmo acontecerá se ocorrer um erro durante seu processamento.

:::

### Exemplo

Ejemplo del método base `On Web Authentication` en [Modo DIGEST](#digest-protocol):

```4d
 // On Web Authentication Database Method
 #DECLARE ($url : Text; $header : Text; $ipB : Text; $ipS : Text; \
 	$user : Text; $pw : Text) -> $valid : Boolean
  
 var $found : cs.WebUserSelection
 $valid:=False

 $found:=ds.WebUser.query("User === :1";$user)
 If($found.length=1) // User is found
 	$valid:=WEB Validate digest($user;[WebUser]password)
 Else
    $valid:=False // User does not exist
 End if
```
