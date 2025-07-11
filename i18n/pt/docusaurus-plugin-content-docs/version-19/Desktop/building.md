---
id: building
title: Criação de um pacote projeto
---

4D inclui um gerador de aplicativos para criar um pacote de projeto (versão final). Esse gerador simplifica o processo de finalização e desenvolvimento de aplicativos compilados 4D. Trata automaticamente as funcionalidades específicas de diferentes sistemas operacionais e facilita a implementação de aplicações cliente-servidor.

O construtor de aplicações permite-lhe:

* Gerar um banco de dados compilado, sem código interpretado
* Construir uma aplicação autônoma, de duplo clique, *i.e.*, fundida com 4D Volume Desktop, o motor de banco de dados 4D,
* Gerar aplicações diferentes a partir do mesmo banco de dados compilado mediante um projeto XML,
* Criar aplicações cliente-servidor homogêneas,
* Construir aplicações cliente-servidor com atualização automática de partes do cliente e do servidor.
* Salve seus parâmetros de geração para uso futuro (botão *Salvar parâmetros*).

> As aplicações compiladas baseiam-se em ficheiros [.4dz](#build-compiled-structure) que são **só de leitura**. Tenha em atenção que a utilização de comandos ou funções que modificam os ficheiros de origem (como `CREATE INDEX` ou `CREATE TABLE` (SQL)) não é possível por padrão em aplicações compiladas. No entanto, pode criar aplicações específicas que suportem modificações locais utilizando a chave XML `PackProject` (ver [doc.4d.com](https://doc.4d.com)).

## Visão geral do aplicativo gerador de aplicações

A cria de um pacote de projetos pode ser efetuada utilizando:

* o comando [BUILD APPLICATION](https://doc.4d.com/4Dv17R6/4D/17-R6/BUILD-APPLICATION.301-4311300.en.html),
* ou a janela **Gerador de aplicações**.

Para exibir o diálogo Build Application , selecione **Design** > **Build Application...** na barra de menu.

![](../assets/en/Project/buildappProj.png)

A caixa de diálogo Criar aplicação inclui várias páginas que podem ser acedidas através de separadores:

![](../assets/en/Project/appbuilderProj.png)

A geração do banco de dados só pode ser realizado quando o banco de dados for compilado. Se selecionar esse comando sem ter previamente compilado o banco de dados, ou no caso do código compilado não for correspondente ao código interpretado, aparece uma caixa de diálogo de advertência que indica que o banco de dados deve ser (re)compilado.

### Parâmetros do gerador de aplicações

Cada parâmetro de geração da aplicação é armazenado como uma chave XML no arquivo da aplicação chamada `buildApp.4DSettings`, localizado na pasta `Settings` do projeto.

Os parâmetros padrão são utilizados na primeira vez que a caixa de diálogo Criar aplicação é utilizada. O conteúdo do ficheiro é atualizado, se necessário, quando se clica em **Criar** ou **Salvar os parâmetros**. Pode definir vários outros ficheiros de parâmetros XML para o mesmo projeto e utilizá-los utilizando o comando [BUILD APPLICATION](https://doc.4d.com/4dv19/help/command/en/page871.html).

As chaves XML oferecem opções adicionais além daquelas exibidas na caixa de diálogo Criar aplicativo. XML keys provide additional options besides those displayed in the Build Application dialog box.

### Arquivo histórico

Quando uma aplicação é construída, 4D gera um arquivo de histórico na pasta **Logs**. O arquivo de registro armazena as seguintes informações para cada compilação:

* O início e o fim da construção de objetivos,
* O nome e o caminho de acesso completo dos ficheiros gerados,
* A data e a hora da geração,
* Todos os erros que forem produzidos.
* Quaisquer problemas de assinatura (por exemplo, um plug-in não assinado).

A verificação desse arquivo pode ajudá-lo a economizar tempo durante as etapas de implantação subsequentes, por exemplo, se você pretende notarizar o aplicativo.

> Use o comando `Get 4D file (Build application log file)` para obter o local do arquivo de registro.

## Nome da aplicação e pasta de destino

![](../assets/en/Project/buidappstructureProj.png)

Digite o nome do aplicativo em **Application Name**.

Especifique a pasta para o aplicativo criado em **Destination Folder (Pasta de destino)**. Se a pasta especificada ainda não existir, o 4D criará uma pasta *Build* para você.

## Página de estrutura compilada

Essa guia permite que você crie um arquivo de estrutura compilado padrão ou um componente compilado:

![](../assets/en/Project/appbuilderProj.png)

### Construir a estrutura compilada

Gera um banco de dados que contém apenas código compilado.

Esta funcionalidade cria um arquivo `.4dz`na pasta `Banco de dados compilado /<project name>`. Por exemplo, se nomeou a sua aplicação como "MyProject", 4D irá criar:

*<destination\>/Compiled Database/MyProject/MyProject.4dz*

> Um arquivo .4dz é essencialmente uma versão compactada da pasta do projeto. A .4dz file is essentially a zipped (packed) version of the project folder. O tamanho compacto e otimizado dos arquivos .4dz torna os pacotes de projeto fáceis de implantar.

#### Incluir pastas relacionadas

Quando se marca esta opção, todas as pastas relacionadas com o banco de dados na pasta Build como pastas *Components* e *Resources*. Para saber mais sobre essas pastas, consulte [Arquitetura do banco de dados](https://livedoc.4d.com/4D-Design-Reference-18/Managing-4D-databases/Description-of-4D-files.300-4575698.en.html#100374).

### Gerar um componente

Constrói um componente compilado a partir da estrutura.

Um componente é um projeto padrão 4D onde foram desenvolvidas funcionalidades específicas. A component is a standard 4D project in which specific functionalities have been developed.

Se tiver nomeado sua aplicação, *MeuComponente*, 4D criará uma pasta Components que contém a pasta *MeuComponente.4dbase*:

\<destination>/Components/name.4dbase/\<name>.4DZ

A pasta *MyComponent.4dbase* contém:

* arquivo **MyComponent.4DZ**
* Uma pasta *Resources* - quaisquer Recursos associados são automaticamente copiados para esta pasta. Quaisquer outros componentes e/ou pastas de plug-ins não são copiados (um componente não pode utilizar plug-ins ou outros componentes).

## Página Aplicação

Essa guia permite que você crie uma versão autônoma e de usuário único do seu aplicativo:

![](../assets/en/Project/standaloneProj.png)

### Criar uma aplicação autónoma

Marcar a opção **Construir aplicação autônoma** e clicar em **Construir** criará uma aplicação autônoma (clicável duas vezes) diretamente do seu projeto de aplicação.

Os seguintes elementos são necessários para a construção:

* 4D Volume Desktop (o motor de base de dados 4D),
* uma [licença apropriada](#licenses)

No Windows, esta funcionalidade cria um ficheiro executável (.exe). Em macOS, trata da criação de pacotes de software.

O princípio consiste em fundir um ficheiro de estrutura compilado com 4D Volume Desktop. A funcionalidade fornecida pelo ficheiro 4D Volume Desktop está ligada à oferta do produto a que se subscreveu. Para mais informações sobre este ponto, consulte a documentação de vendas e a [4D Store](http://www.4d.com/).

Você pode definir um arquivo de dados padrão ou permitir que os usuários criem e usem seu próprio arquivo de dados (consulte o gerenciamento [de arquivos de dados na seção de aplicativos finais](https://doc.4d.com/4Dv17R6/4D/17-R6/Data-file-management-in-final-applications.300-4354729.en.html)).

É possível automatizar a atualização de aplicativos de usuário único mesclados através de uma sequência de comandos de idioma (veja [Atualização automática de aplicativos de servidor ou de usuário único](https://doc.4d.com/4Dv17R6/4D/17-R6/Automatic-updating-of-server-or-single-user-applications.300-4354721.en.html).

#### Localização do 4D Volume Desktop

Para construir uma aplicação independente, você deve primeiro designar a pasta que contém o arquivo da área de trabalho do volume 4D:

* *Windows* - a pasta contém o 4D Volume Desktop.4DE, 4D Volume Desktop.RSR, bem como vários arquivos e pastas necessários para sua operação. Esses itens devem ser colocados no mesmo nível da pasta selecionada.
* *macOS* - 4D Volume Desktop é fornecido na forma de um pacote de software estruturado que contém vários arquivos genéricos e pastas.

Para selecionar a pasta Desktop de volume 4D, clique no botão **[...]**. Uma caixa de diálogo aparece permitindo que você designe a pasta 4D Volume Desktop (Windows) ou pacote (macOS).

Depois que a pasta for selecionada, o nome completo do caminho será exibido e, se realmente conter 4D Volume Desktop, a opção para a construção de uma aplicação executável é ativada.

> O número da versão do 4D Volume Desktop deve corresponder ao número da versão do 4D Developer Edition. Por exemplo, se você usar o 4D Developer v18, deverá selecionar um 4D Volume Desktop v18.

#### Modo de ligação de dados

Esta opção permite escolher o modo de ligação entre o aplicativo mesclado e o arquivo de dados local. Estão disponíveis dois modos de ligação de dados:

* **Por nome da aplicação** (por defeito) - A aplicação 4D abre automaticamente o ficheiro de dados mais recentemente aberto correspondente ao ficheiro de estrutura. Isto permite-lhe mover o pacote de aplicações livremente no disco. Esta opção deve ser geralmente utilizada para aplicações fundidas, a menos que seja especificamente necessário duplicar a aplicação.

* **Por caminho do aplicativo** - O aplicativo 4D mesclado analisará o arquivo *lastDataPath.xml* do aplicativo e tentará abrir o arquivo de dados com um atributo "executablePath" que corresponda ao caminho completo do aplicativo. Se tal entrada for encontrada, o arquivo de dados correspondente (definido através do seu atributo "dataFilePath") será aberto. Caso contrário, o último arquivo de dados aberto será aberto (modo padrão).

Para obter mais informações sobre o modo de ligação de dados, consulte [Último arquivo de dados aberto](#last-data-file-opened).

#### Ficheiros gerados

Quando você clicar no botão **Construa** , A 4D cria automaticamente uma pasta **Aplicação Final** na pasta de Destino **** especificada. Dentro da pasta de Aplicação Final está uma subpasta com o nome do aplicativo especificado nele.

Se você tiver especificado "MyProject" como o nome do aplicativo, encontrará os seguintes arquivos nessa subpasta (também conhecida como MyProject):

* *Windows*
  * MyProject.exe - Seu executável e um MyProject.rsr (os recursos da aplicação)
  * Pasta 4D Extensions, pasta Resources, várias bibliotecas (DLL), pasta Native Components, pasta SASL Plugins - Arquivos necessários para a operação do aplicativo
  * Uma pasta Database - Inclui uma pasta Resources e um arquivo MyProject.4DZ. Database folder  - Includes a Resources folder and  MyProject.4DZ file. **Note**: esta pasta também contém a pasta *Dados padrão*, se tiver sido definido (ver [Gerenciamento de arquivos de dados em aplicativos finais](#management-of-data-files).
  * (Opcional) Pasta Components e/ou pasta Plugins - Contém todos os componentes e/ou arquivos de plug-in incluídos no banco de dados. Para obter mais informações sobre isso, consulte os plugins [e componentes](#plugins--components-page).
  * Pasta de licenças - Um arquivo XML com números de licença integrados ao aplicativo. Para obter mais informações sobre isso, consulte a seção [Licenses & Certificate](#licenses--certificate-page) .
  * Itens adicionais adicionados à pasta da Área de Trabalho de Volume 4D, se houver (veja [Personalizando a pasta de Volume 4D para Desktop](#customizing-4d-volume-desktop-folder)).

 Todos estes itens devem ser mantidos na mesma pasta para que o executável possa operar.

* *macOS*
  * Um pacote de software chamado MyProject.app que contém seu aplicativo e todos os itens necessários para sua operação, incluindo os plug-ins, componentes e licenças. Para obter mais informações sobre a integração de plug-ins e componentes, consulte a seção [Plugins e componentes](#plugins--components-page). Para obter mais informações sobre a integração de licenças, consulte a seção [Licenças e Certificado](#licenses--certificate-page). **Nota**: No macOS, o comando [Application file](https://doc.4d.com/4Dv18R4/4D/18-R4/Application-file.301-4982855.en.html) do idioma 4D retorna o caminho do arquivo ApplicationName (localizado na pasta Contents:macOS do pacote do software) e não o do arquivo .comp (Pasta Contents:Resources do pacote de software).

#### Personalização da pasta 4D Volume Desktop

Ao criar um aplicativo autônomo, o 4D copia o conteúdo da pasta 4D Volume Desktop para a pasta Destination > *Final Application* . Então, você será capaz de personalizar o conteúdo da pasta original de volume da área de trabalho 4D de acordo com suas necessidades. Pode, por exemplo:

* Instalar uma versão 4D Volume Desktop correspondente a um idioma específico;
* Adicionar uma pasta personalizada *PlugIns*;
* Construir um pacote de projeto
> Construir um pacote de projeto > Construir um pacote de projeto > No macOS, o 4D Volume Desktop é fornecido na forma de um pacote de software. Para modificá-lo, primeiro é preciso exibir seu conteúdo (**Control+clique** no ícone).

#### Localização dos arquivos da Web

Se o seu aplicativo autônomo for usado como um servidor Web, os arquivos e pastas exigidos pelo servidor devem ser instalados em locais específicos. Estes itens são os seguintes:

* *cert.pem* e *key.pem* arquivos (opcional): Esses arquivos são usados para conexões TLS e por comandos de criptografia de dados,
* pasta raiz Web padrão.

Os elementos devem ser instalados:

* **no Windows**: na *Aplicação Final\MyProject\Database*.
* **no macOS**: ao lado do pacote de software *MyProject.app*.

## Página cliente/servidor

Nessa guia, você pode criar aplicativos cliente-servidor personalizados que sejam homogêneos, multiplataforma e com uma opção de atualização automática.

![](../assets/en/Project/buildappCSProj.png)

### O que é uma aplicação Cliente/Servidor?

Uma aplicação cliente/servidor provém da combinação de três itens:

* A compiled 4D database,
* A aplicação 4D Server,
* A aplicação 4D Volume Desktop (macOS e/ou Windows).

Uma vez criado, um aplicativo cliente/servidor é composto de duas partes personalizadas: a parte do servidor (exclusiva) e a parte do cliente (a ser instalada em cada máquina cliente).

> Se quiser lançar uma aplicação cliente-servidor em um ambiente heterogêneo (aplicações de clliente rodando em Intel/AMD e Apple Silicon), é recomendado  [compilar o projeto para todos os processsadores](Project/compiler.md#compilation-target) em uma máquina macOS, de forma que todas as aplicações cliente rodem nativamente.

Além disso, o aplicativo cliente/servidor é personalizado e fácil de usar:

* Para iniciar a parte do servidor, o usuário simplesmente clica duas vezes no aplicativo do servidor. The database does not need to be selected.
* Para iniciar a parte do cliente, o usuário simplesmente clica duas vezes no aplicativo cliente, que se conecta diretamente ao aplicativo do servidor. Você não precisa escolher um servidor em uma caixa de diálogo de conexão. O cliente direciona o servidor usando seu nome, quando o cliente e o servidor estão na mesma sub-rede, ou usando seu endereço IP, que é definido usando a chave `IPAddress` XML no arquivo buildapp.4DSettings. Se a conexão falhar, mecanismos alternativos específicos do [podem ser implementados](#management-of-client-connections). Você pode "forçar" a exibição da caixa de diálogo de conexão padrão segurando a tecla **Opção** (macOS) ou **Alt** (Windows) enquanto inicia a aplicação cliente. Apenas a parte do cliente pode conectar à parte do servidor correspondente. Se um usuário tentar conectar à parte do servidor usando uma aplicação 4D padrão, uma mensagem de erro é retornada e a conexão é impossível.
* Um aplicativo cliente/servidor pode ser definido para que a parte do cliente [possa ser atualizada automaticamente através da rede](#copy-of-client-applications-inside-the-server-application). Você só precisa criar e distribuir uma versão inicial do aplicativo cliente, atualizações subsequentes são tratadas usando o mecanismo de atualização automática.
* Também é possível automatizar a atualização da parte do servidor por meio do uso de uma sequência de comandos da linguagem ([SET UPDATE FOLDER](https://doc.4d.com/4dv19/help/command/en/page1291.html) e [RESTART 4D](https://doc.4d.com/4dv19/help/command/en/page1292.html)).

### Criar aplicação servidor

Marque esta opção para gerar a parte do servidor da sua aplicação durante a fase de construção. Você deve designar a localização em seu disco da aplicação 4D Server para ser usado. Esse servidor 4D deve corresponder à plataforma atual (que também será a plataforma do aplicativo do servidor).

#### Localização do 4D Server

Clique no botão **[...]** e use *Procurar pasta* para localizar o aplicativo 4D Server No macOS, deve selecionar o pacote 4D Server diretamente. No macOS, deve selecionar o pacote 4D Server diretamente.

#### Versão atual

Utilizado para indicar o número da versão atual da aplicação gerada. Pode então aceitar ou rejeitar ligações de aplicações cliente conforme o seu número de versão. O intervalo de compatibilidade para aplicações cliente e servidor é estabelecido usando [XML keys](#build-application-settings).

#### Modo de ligação de dados

Esta opção permite escolher o modo de ligação entre o aplicativo mesclado e o arquivo de dados local. Estão disponíveis dois modos de ligação de dados:

* **Por nome da aplicação** (por defeito) - A aplicação 4D abre automaticamente o ficheiro de dados mais recentemente aberto correspondente ao ficheiro de estrutura. Isto permite-lhe mover o pacote de aplicações livremente no disco. Esta opção deve ser geralmente utilizada para aplicações fundidas, a menos que seja especificamente necessário duplicar a aplicação.

* **Por caminho do aplicativo** - O aplicativo 4D mesclado analisará o arquivo *lastDataPath.xml* do aplicativo e tentará abrir o arquivo de dados com um atributo "executablePath" que corresponda ao caminho completo do aplicativo. Se tal entrada for encontrada, o arquivo de dados correspondente (definido através do seu atributo "dataFilePath") será aberto. Caso contrário, o último arquivo de dados aberto será aberto (modo padrão).

Para obter mais informações sobre o modo de ligação de dados, consulte [Último arquivo de dados aberto](#last-data-file-opened).

### Criar a aplicação cliente

Marcar esta opção gera a parte do cliente da sua aplicação durante a fase de construção.

Pode selecionar esta opção:

* Juntamente com a opção [**Build server application**](#build-server-application) para construir partes correspondentes de servidor e cliente para a plataforma atual e (opcionalmente) incluem os arquivos de arquivo de atualização automática.
* sem selecionar a opção [**Construa a aplicação de servidor**](#build-server-application) geralmente para construir o arquivo de atualização a ser selecionado a partir da plataforma "simultânea" ao construir a parte do servidor.

#### Localização do 4D Volume Desktop

Designa a localização no seu disco da aplicação 4D Volume Desktop a ser usada para construir a parte cliente da sua aplicação.

> O número da versão do 4D Volume Desktop deve corresponder ao número da versão do 4D Developer Edition. Por exemplo, se você usar 4D v19, você deve selecionar um volume 4D na área de trabalho v19.

A Área de Trabalho de Volume 4D deve corresponder à plataforma atual (que também será a plataforma do aplicativo cliente). Se você deseja criar um aplicativo cliente para a plataforma "simultânea", você deve realizar uma operação de construção adicional usando uma aplicação 4D em execução nessa plataforma.

Se você deseja que o aplicativo cliente se conecte ao servidor usando um endereço específico (diferente do nome do servidor publicado na sub-rede), você deve usar a chave `IPAddress` XML no aplicativo buildapp. Para mais informações sobre este arquivo, consulte a descrição do comando [`CONSTRUIR APLICAÇÃO`](https://doc.4d.com/4dv19/help/command/en/page871.html). Você também pode implementar mecanismos específicos em caso de falha na conexão. Os diferentes cenários propostos são descritos no parágrafo [Gerenciamento de conexões por aplicativos cliente](#management-of-client-connections).

#### Cópia de aplicativos cliente dentro do aplicativo servidor

As opções desta área configuram o mecanismo para atualizar as partes do cliente do(s) seus aplicativos cliente/servidor usando a rede toda vez que uma nova versão do aplicativo for gerada. Estas opções só são ativadas quando a opção **cliente de compilação** é marcada.

* **Permitir atualização automática da aplicação cliente Windows** - Marque esta opção para construir um `.4darchive` que pode ser enviado para as aplicações cliente na plataforma Windows em caso de atualização.
* **Permitir atualização automática do aplicativo cliente Macintosh** - Marque esta opção para construir um `. arquivo darchive` que pode ser enviado para os seus aplicativos cliente na plataforma Macintosh em caso de atualização.

O ficheiro `.4darchive` é copiado para a seguinte localização:

```
<ApplicationName>_Build/Client Server executable/Upgrade4DClient/
```

#### Seleção do arquivo cliente para a plataforma concorrente

Você pode marcar a opção **Permitir atualização automática...** para aplicativos clientes em execução na plataforma simultânea. Esta opção só é activada se:

* a opção **Build server application** é verificada
* a opção **Permitir atualização automática...** para aplicativos clientes que executam na plataforma atual está marcada.

Esta funcionalidade requer que clique no botão **[...]** e designe a localização no disco do ficheiro a utilizar para a atualização. O ficheiro a selecionar depende da plataforma do servidor atual:

| Plataforma de servidor actual | Ficheiro obrigatório                                         | Detalhes                                                                                                                                                                                       |
| ----------------------------- | ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| macOS                         | Windows 4D Volume Desktop *ou* Windows client update archive | Por padrão, é selecionada a aplicação `4D Volume Desktop` para Windows. Para selecionar um arquivo `.4darchive` previamente construído no Windows, pressione **Shift** enquanto clica no [...] |
| Windows                       | macOS client update archive                                  | Selecione um arquivo `.4darchive` assinado, criado anteriormente no macOS                                                                                                                      |

Pode construir um arquivo `.4darchive` na plataforma selecionado apenas [**Criar aplicação cliente**](#build-client-application) e a opção [**Permitir atualização automática...**](#copy-of-client-applications-inside-the-server-application).

#### Mostrar notificação de atualização

A notificação de atualização da aplicação cliente é realizada automaticamente após a atualização da aplicação do servidor.

Funciona da seguinte forma: quando uma nova versão do cliente/servidor de aplicação é feita usando o construtor de aplicação, a parte do novo cliente será copiada como um arquivo compactado na subpasta **Upgrade4DClient** da pasta do Servidor **ApplicationName** (no macOS, estas pastas estão incluídas no pacote do servidor). Se você seguiu o processo de geração de um aplicativo cliente multiplataforma, uma . O arquivo de atualização*4darchive* está disponível para cada plataforma:

Para acionar notificações de atualização de aplicativo cliente, basta substituir a versão antiga do aplicativo servidor pelo novo e, em seguida, executá-lo. O resto do processo é automático.

Do lado do cliente, quando a aplicação cliente "antiga" tenta conectar-se à aplicação servidor atualizada, se mostra uma caixa de diálogo na máquina cliente, indicando que há uma nova versão disponível. O utilizador pode tanto actualizar a sua versão como cancelar a caixa de diálogo.

* Se o utilizador clicar em **OK**, a nova versão é descarregada para a máquina cliente através da rede. Uma vez terminado o download, a antiga aplicação cliente é fechada e a nova versão é lançada e liga-se ao servidor. A versão antiga da aplicação é então colocada na lixeira da máquina.
* Se o usuário clicar em **Cancelar**, a atualização será cancelada; se a versão antiga do aplicativo cliente não estiver na gama de versões aceitas pelo servidor (por favor, consulte o parágrafo a seguir), o aplicativo está fechado e a conexão é impossível. Caso contrário (por defeito), a ligação é estabelecida.

#### Forçar atualizações automáticas

Em alguns casos, poderá querer impedir que as aplicações cliente possam cancelar a transferência da atualização. Por exemplo, se usou uma nova versão da aplicação fonte 4D Server, a nova versão da aplicação cliente deve absolutamente ser instalada em cada máquina cliente.

Para forçar a atualização, basta excluir o número da versão atual das aplicações cliente (X-1 e anteriores) no intervalo de números de versão compatível com a aplicação do servidor. Neste caso, o mecanismo de atualização não permitirá a conexão de aplicativos cliente não atualizados. Por exemplo, se a nova versão do aplicativo cliente-servidor for 6, pode estipular-se que qualquer aplicativo cliente com um número de versão inferior a 6 não será autorizado a ligar.

O número da versão [atual](#current-version) é definido na página do Cliente/Servidor da caixa de diálogo da aplicação de construção. Os intervalos de números autorizados estão definidos no projeto de aplicação usando as chaves [XML específicas](#build-application-settings).

#### Erro de actualização

Se 4D não puder realizar a atualização do aplicativo cliente, a máquina do cliente exibe a seguinte mensagem de erro: "A atualização da aplicação do cliente falhou. A aplicação vai agora desistir."

Existem muitas causas possíveis para este erro. Quando você receber esta mensagem, é aconselhável verificar os seguintes parâmetros primeiro:

* **Pathnames** - Verifique a validade dos pathnames definidos no projeto de aplicação através da caixa de diálogo do Construtor de Aplicação ou via chaves XML (por exemplo *ClientMacFolderToWin*). Em particular, verifique os caminhos para as versões do 4D Volume Desktop.
* **privilégios de leitura/gravação** - Na máquina do cliente, verifique se o usuário atual tem direitos de acesso de gravação para a atualização da aplicação do cliente.

### Ficheiros gerados

Uma vez que uma aplicação cliente/servidor é criada, você encontrará uma nova pasta na pasta de destino chamada **Client Server executable**. Esta pasta contém duas subpastas, `<ApplicationName>Client` e `<ApplicationName>Server`.
> Estas pastas não são geradas se ocorrer um erro. Neste caso, abra o arquivo [log](#log-file) para descobrir a causa do erro.

A pasta `<ApplicationName>Cliente` contém a porção do cliente do aplicativo correspondente à plataforma de execução do construtor de aplicativo. Esta pasta deve ser instalada em cada máquina do cliente. A pasta `<ApplicationName>Server` contém a parte do servidor da aplicação.

O conteúdo dessas pastas varia dependendo da plataforma atual:

* *Windows* - Cada pasta contém o arquivo executável do aplicativo, chamado `<ApplicationName>Cliente. xxeque` para a parte do cliente e o servidor `<ApplicationName>. xe` para a parte do servidor bem como os correspondentes arquivos .rsr. As pastas também contêm vários arquivos e pastas necessários para que os aplicativos funcionem e itens personalizados que podem estar na pasta de Volume 4D e no Servidor 4D.
* *macOS* - Cada pasta contém apenas o pacote de aplicação, chamado `<ApplicationName> Client` para a parte do cliente e `<ApplicationName> Server` para a parte do servidor. Cada pacote contém todos os itens necessários para que a aplicação funcione. No macOS, inicie um pacote fazendo duplo clique no mesmo.

 > Os pacotes macOS construídos contêm os mesmos itens que as subpastas do Windows. Você pode exibir seu conteúdo (**Control+click** no ícone para poder modificá-los.

Se você marcou a opção "Permitir atualização automática do aplicativo cliente", uma subpasta adicional chamada *Upgrade4DClient* é adicionada na pasta/pacote do servidor `<ApplicationName>`. Esta subpasta contém o aplicativo cliente no macOS e/ou no formato Windows como um arquivo compactado. Este ficheiro é utilizado durante a atualização automática das aplicações clientes.

#### Localização dos arquivos da Web

Se o servidor e/ou cliente parte do seu aplicativo clicável duplo for usado como um servidor web, os arquivos e pastas exigidos pelo servidor devem ser instalados em locais específicos. Estes itens são os seguintes:

* *arquivos cert.pem* e *key.pem* (opcional): Esses arquivos são usados para conexões SSL e por comandos de criptografia de dados,
* Pasta raiz Web por defeito (WebFolder).

Os elementos devem ser instalados:

* **em Windows**
  * **Aplicação do servidor** - na subpasta `Client Server
executable\&#060;ApplicationName&#062;Server\Server Database`.
  * **Aplicación cliente** - na subpasta `Client Server executable\&#060;ApplicationName&#062;Client`.

* **no macOS**
  * **Aplicação do servidor** - com o pacote de software `<ApplicationName>Server`.
  * **Aplicação cliente** - ao lado do pacote de software `<ApplicationName>Client`.

### Incorporar uma aplicação cliente usuário único

4D lhe permite incorporar uma estrutura compilada na aplicação cliente. Esse recurso pode ser usado, por exemplo, para fornecer aos usuários um aplicativo "portal", que dá acesso a diferentes aplicativos de servidor graças ao comando `OPEN DATABASE` executando um `. arquivo dlink`

Para ativar este recurso, adicione as chaves `DatabaseToEmbedInClientWinFolder` e/ou `DatabaseToEmbedInClientMacFolder` no arquivo de configurações do *buildApp*. Quando uma das chaves estiver presente, a aplicação cliente gera uma aplicação monousuário: a estrutura compilada, ao inves do arquivo *EnginedServer.4Dlink* é colocada na pasta "Database".

* Se existir uma pasta de dados padrão no aplicativo de usuário único, uma licença será incorporada.
* Se não existir uma pasta de dados padrão no aplicativo de usuário único, ela será executada sem arquivo de dados e sem licença.

O cenário básico é o seguinte:

1. Na caixa de diálogo da Aplicação de Construção, selecione a opção "Construir estrutura compilada" para produzir um . DZ ou .4DC para o aplicativo a ser usado em modo de usuário único.
2. No *aplicativo da construção. DSettings* arquivo da aplicação cliente-servidor, use o seguinte xml chave(s) para indicar o caminho para a pasta que contém a compilação de aplicação de único usuário:

* `DatabaseToEmbedInClientWinFolder`
* `DatabaseToEmbedInClientMacFolder`

3. Construir a aplicação cliente-servidor. Isto terá os seguintes efeitos:

* toda a pasta do aplicativo do único usuário é copiada dentro da pasta "Database" do cliente mesclado
* o ficheiro *EnginedServer.4Dlink* da pasta "Database" não é gerado
* o .4DC, .4DZ, .4DIndy arquivos da cópia do aplicativo de usuário único são renomeados usando o nome do cliente mesclado
* a chave `PublishName` não foi copiada no *info.plist* do cliente mesclado
* Se o aplicativo de usuário único não tiver uma pasta "Dados padrão", o cliente mesclado será executado sem dados.

Atualização automática de 4D Server ([Current version](#current-version), comando `SET UPDATE FOLDER` ...) com aplicação monousuário com aplicação remoto padrão Em conexão, o aplicativo de usuário único compara sua chave `Atuais` com o intervalo de versão do 4D Server Se fora do intervalo, o aplicativo cliente atualizado será baixado do servidor e o atualizador iniciará o processo de atualização local. Em conexão, o aplicativo de usuário único compara sua chave `Atuais` com o intervalo de versão do 4D Server Se fora do intervalo, o aplicativo cliente atualizado será baixado do servidor e o atualizador iniciará o processo de atualização local. Se fora do intervalo, o aplicativo cliente atualizado será baixado do servidor e o atualizador iniciará o processo de atualização local.

### Personalização dos nomes da pasta de cache cliente e/ou servidor

Pastas de cache de cliente e servidor são usadas para armazenar elementos compartilhados como recursos ou componentes. Eles são necessários para gerenciar as trocas entre o servidor e os clientes remotos. Aplicações cliente/servidor usam caminhos padrão para as pastas de cache do sistema de cliente e servidor.

Em alguns casos específicos, talvez seja necessário personalizar os nomes dessas pastas para implementar arquiteturas específicas (veja abaixo). 4D fornece chaves `ClientServerFolderName` e `ServerStructureFolderName` a serem definidas no arquivo de configurações do *buildApp*.

#### Pasta de cache cliente

Personalizar o nome da pasta de cache do lado do cliente pode ser útil quando sua aplicação do cliente é usada para se conectar a vários servidores mesclados que são similares, mas usam conjuntos de dados diferentes. Neste caso, para salvar vários downloads desnecessários de recursos locais idênticos, você pode usar a mesma pasta de cache local personalizada.

* Configuração padrão (*para cada conexão para um servidor, uma pasta cache é baixada ou atualizada*):

![](../assets/en/Admin/cachea.png)

* Usando a chave `ClientServerFolderName` (*uma única pasta de cache é usada para todos os servidores*):

![](../assets/en/Admin/cacheb.png)

#### Pasta de cache do servidor

Personalizar o nome da pasta de cache no lado do servidor é útil quando você executa vários aplicativos de servidor idênticos criados com diferentes versões 4D no mesmo computador. Se você quiser que cada servidor use seu próprio conjunto de recursos, você precisará personalizar a pasta de cache do servidor.

* Configuração padrão (*mesmo servidor aplicativos compartilham a mesma pasta de cache*:

![](../assets/en/Admin/cacheServera.png)

* Usar a chave `ServerStructureFolderName` (*uma pasta cache é usada para cada aplicação de servidor*):

![](../assets/en/Admin/cacheServerb.png)

## Página Plugins e componentes

Nesta aba, você define cada [plug-in](Concepts/plug-ins.md) e cada componente [](Concepts/components.md) que você usará em sua aplicação autônoma ou cliente/servidor.

A página lista os elementos carregados pela aplicação 4D atual:

![](../assets/en/Project/buildapppluginsProj.png)

* Coluna **Active** - Indica que os itens serão integrados no pacote de aplicação compilado. Todos os itens são marcados por padrão. Para excluir um plug-in ou um componente, desmarque a caixa de seleção ao lado dele.

* **Plugins e componentes** coluna - Exibe o nome do plug-in/component.

* **ID** coluna - Exibe o número de identificação do plug-in/componente (se houver).

* A coluna **Type** - Indica o tipo de item: plug-in ou componente.

Se você quer integrar outros plugins ou componentes na aplicação executável, você só precisa colocá-los em uma pasta **PlugIns** ou **Components** ao lado da aplicação 4D Volume Desktop ou ao lado da aplicação 4D Server O mecanismo para copiar o conteúdo da pasta do aplicativo de origem (ver [Personalizando a pasta desktop de volume 4D](#customizing-4d-volume-desktop-folder)) pode ser usado para integrar qualquer tipo de arquivo na aplicação executável. O mecanismo para copiar o conteúdo da pasta do aplicativo de origem (ver [Personalizando a pasta desktop de volume 4D](#customizing-4d-volume-desktop-folder)) pode ser usado para integrar qualquer tipo de arquivo na aplicação executável.

Se houver um conflito entre duas versões diferentes do mesmo plug-in (uma carregada por 4D e a outra localizada na pasta do aplicativo de origem), prioridade vai para o plug-in instalado na pasta Volume Desktop/4D do Servidor. No entanto, se houver duas instâncias do mesmo componente, o aplicativo não abrirá.
> O uso de plug-ins e/ou componentes em uma versão de desenvolvimento requer os números de licença necessários.

## Página Licenças e certificados

A página Licences & Certificate pode ser utilizada para:

* designar o(s) número(s) da licença que você deseja integrar em seu aplicativo de stand-alone de usuário único
* assinar a aplicação através de um certificado no macOS.

![](../assets/en/Admin/buildappCertif.png)

### Licenças

Esta aba exibe a lista de licenças de implantação disponíveis que você poderá integrar ao seu aplicativo. Por padrão, a lista está vazia. Você deve adicionar explicitamente sua licença *4D Developer Professional* bem como cada licença *4D Desktop Volume* para ser usada na aplicação criada. Você pode adicionar outro número de Profissional de Desenvolvedor 4D e suas licenças associadas, além da que está sendo usada atualmente.

Para remover ou adicionar uma licença, use os botões **[+]** e **[-]** na parte inferior da janela.

Quando você clicar no botão \[+], uma caixa de diálogo 'Abrir arquivo' aparece exibindo por padrão o conteúdo da pasta *Licenças* do seu computador. Para obter mais informações sobre a localização desta pasta, consulte o comando [Get 4D folder](https://doc.4d.com/4Dv17R6/4D/17-R6/Get-4D-folder.301-4311294.en.html).

Você deve designar os arquivos que contêm sua licença de desenvolvedor, bem como os que contém suas licenças de implantação. Esses arquivos foram gerados ou atualizados quando a licença *4D Developer Professional* e as licenças *4D Desktop Volume* foram compradas.

Depois de selecionar um arquivo, a lista indicará as características da licença que ele contém.

* **Licença #** - Número de licença do produto
* **Licença** - Nome do produto
* **Data de expiração** - Data de expiração da licença (se houver)
* **Caminho** - Localização em disco

Se uma licença não for válida, será avisado por uma mensagem.

Pode designar o número de ficheiros válidos que desejar. Ao construir uma aplicação executável, o 4D usará a licença mais apropriada disponível.
> Licenças "R" dedicadas são necessárias para criar aplicativos com base nas versões de "R-release" (números de licença para "R" produtos começam com "R-4DP").

Depois que o aplicativo é construído, um novo arquivo de licença de implantação é automaticamente incluído na pasta Licenças ao lado do aplicativo executável (Windows) ou no pacote (macOS).

### Certificado de assinatura do macOS

O construtor de aplicações pode assinar aplicações 4D mesclados no macOS (aplicações de usuário único, servidor 4D e partes de clientes sob macOS). A assinatura de um aplicativo autoriza que ele seja executado usando a funcionalidade de Gatekeeper do macOS quando a opção "Mac App Store e Desenvolvedores identificados" estiver selecionada (veja "Sobre Gatekeeper" abaixo).

* Marque a opção **Assinar a aplicação** para incluir a certificação no procedimento de construtor de aplicativos para macOS. 4D irá verificar a disponibilidade de elementos necessários para a certificação quando a compilação ocorrer:

![](../assets/en/Admin/buildapposxcertProj.png)

Esta opção é exibida tanto no Windows quanto no macOS, mas apenas é tida em conta para as versões do macOS.

* **Nome do certificado** - Digite o nome do seu certificado de desenvolvedor validado pela Apple nesta área de entrada. O nome do certificado geralmente é o nome do certificado no utilitário Acesso Keychain (parte em vermelho no exemplo a seguir):

![](../assets/en/Project/certificate.png)

Para obter um certificado de desenvolvedor da Apple, Inc., você pode usar os comandos do menu Acesso de Chaves ou vá aqui: [http://developer.apple.com/library/mac/#documentation/Security/Conceptual/CodeSigningGuide/Procedures/Procedures.html](http://developer.apple.com/library/mac/#documentation/Security/Conceptual/CodeSigningGuide/Procedures/Procedures.html).
> Este certificado requer a presença da utilidade do co design da Apple, que é fornecida por padrão e geralmente localizada na pasta "/usr/bin/". Se ocorrer um erro, verifique se este utilitário está presente em seu disco.

* **Gerar certificado auto-assinado** - executa o "Assistente de Certificado" que permite gerar um certificado auto-assinado. Se você não tiver um certificado de desenvolvedor da Apple, você precisará fornecer um certificado auto-assinado. Com este certificado, nenhuma mensagem de alerta é exibida se a aplicação for implementada internamente. Se a aplicação é implantada externamente (por exemplo, através de http ou e-mail), na inicialização do macOS exibe uma mensagem de alerta de que o desenvolvedor da aplicação é não identificado. O usuário pode "forçar" a abertura da aplicação. No "Certificado de Assistente", certifique-se de selecionar as opções apropriadas: ![](../assets/en/Admin/Cert1.png) ![](../assets/en/Admin/Cert2.png)

> 4D recomenda assinar o Programa de Desenvolvimento da Apple para obter acesso a Certificados de Desenvolvedor que são necessários para notarizar aplicativos (veja abaixo).

#### Sobre Gatekeeper

O Gatekeeper é um recurso de segurança do macOS que controla a execução de aplicativos baixados da Internet. Se um aplicativo baixado não vem da Apple Store ou não estiver assinado, será rejeitado e não poderá ser iniciado.

A opção **Assinar a aplicação** no Gerador de aplicações 4D permite que você gere aplicações compatíveis com essa opção por padrão.

#### Sobre a notarização

A notarização de aplicação é altamente recomendada pela Apple a partir do macOS 10.14.5 (Mojave) e 10. 5 (Catalina), pois aplicativos não notariados implantados através da internet são bloqueados por padrão.

A partir de 4D v18, as [funções de assinatura integrada](#macos-signing-certificate) foram atualizadas para atender a todos os requisitos da Apple para permitir o uso do serviço de reconhecimento de firma da Apple. A notarização em si deve ser conduzida pelo desenvolvedor e é independente da 4D (note também que ela requer a instalação do Xcode). Veja [o blog](https://blog.4d.com/how-to-notarize-your-merged-4d-application/)com uma descrição do processo de notarização.

Para obter mais informações sobre o conceito de notarização, consulte [nesta página no site de desenvolvedores Apple](https://developer.apple.com/documentation/xcode/notarizing_your_app_before_distribution/customizing_the_notarization_workflow).

## Personalizar ícones de uma aplicação

4D associa um ícone padrão com sistema autônomo, servidor e aplicativos clientes, no entanto, você pode personalizar o ícone para cada aplicativo.

* **macOs** - Ao construir uma aplicação com duplo clique, 4D lida com a personalização do ícone. Para fazer isso, você deve criar um arquivo de ícone (tipo de icns), antes de criar o arquivo do aplicativo, e colocá-lo ao lado da pasta do projeto.
> A Apple, Inc. fornece uma ferramenta específica para construir arquivos de ícones *icns* (para mais informações, consulte a documentação da [Apple](https://developer.apple.com/library/archive/documentation/GraphicsAnimation/Conceptual/HighResolutionOSX/Optimizing/Optimizing.html#//apple_ref/doc/uid/TP40012302-CH7-SW2)).

 Seu arquivo de ícone deve ter o mesmo nome do arquivo de projeto e incluir a extensão *.ico*. 4D leva automaticamente este arquivo em conta ao construir o aplicativo clicável duplo (o arquivo *.icns* é renomeado *ApplicationName.

* **Windows** - Ao construir uma aplicação clicável e dupla, o 4D lida com a personalização do seu ícone. Para fazer isso, você deve criar um arquivo de ícone (*. extensão co* , antes de construir o arquivo do aplicativo e colocá-lo ao lado da pasta do projeto.

 Seu arquivo de ícone deve ter o mesmo nome do arquivo de projeto e incluir a extensão *.icns*. 4D leva automaticamente este arquivo em conta ao construir o aplicativo clicável duplo (o arquivo *.icns* é renomeado *ApplicationName.</p></li> </ul>

Você também pode definir as [chaves XML ](https://doc.4d.com/4Dv17R6/4D/17-R6/4D-XML-Keys-BuildApplication.100-4465602.en.html) específicas no arquivo buildApp.4DSettings para designar cada ícone a ser usado. Estão disponíveis as seguintes chaves:

* RuntimeVLIconWinPath
* RuntimeVLIconMacPath
* ServerIconWinPath
* ServerIconMacPath
* ClientMacIconForMacPath
* ClientWinIconForMacPath
* ClientMacIconForWinPath
* ClientWinIconForWinPath

## Gestão do(s) ficheiro(s) de dados

### Abertura do ficheiro de dados

Quando um usuário lança um aplicativo mesclado ou uma atualização (usuário único ou aplicativo/servidor), 4D tenta selecionar um arquivo de dados válido. A aplicação examina sucessivamente vários locais.

A sequência para o lançamento de uma aplicação fusionada a seguinte:

1. O 4D tenta abrir o último arquivo de dados aberto, [conforme descrito abaixo](#last-data-file-opened) (não se aplica durante o lançamento inicial).
2. Se não for encontrado, 4D tenta abrir o arquivo de dados em uma pasta de dados padrão ao lado do arquivo .4DZ em modo somente leitura.
3. Se não for encontrado, 4D tenta abrir o arquivo de dados padrão (mesmo nome e mesmo local do arquivo .4DZ).
4. Se não for encontrado, 4D mostra uma caixa de diálogo padrão "Abrir ficheiro de dados".

### Último arquivo de dados aberto

#### Caminho do último arquivo de dados

Quaisquer aplicativos autônomos ou de servidor criados com 4D armazenam o caminho do último arquivo de dados aberto na pasta preferências do usuário do aplicativo.

O local da pasta de preferências do usuário da aplicação corresponde ao caminho retornado pela seguinte instrução:

```4d
userPrefs:=Get 4D folder(Pasta 4D activa)
```

O caminho do arquivo de dados é armazenado em um arquivo dedicado, chamado *lastDataPath.xml*.

Graças a esta arquitetura, quando você fornece uma atualização do seu aplicativo, o arquivo de dados do usuário local (último arquivo de dados utilizado) é aberto automaticamente na primeira inicialização.

Este mecanismo é geralmente adequado para implantações padrão. No entanto, para necessidades específicas, por exemplo, se você duplicar seus aplicativos mesclados, você pode querer alterar a forma como o arquivo de dados está vinculado ao aplicativo (descrito abaixo).

#### Configuração do modo de ligação de dados

Com suas aplicações compiladas, o 4D utiliza automaticamente o último arquivo de dados aberto. Por padrão, o caminho do arquivo de dados é armazenado na pasta de preferências do usuário do aplicativo e está vinculado ao nome **da aplicação**.

Isso pode ser inadequado se você quiser duplicar um aplicativo com merge destinado a usar arquivos de dados diferentes. Os aplicativos duplicados realmente compartilham a pasta de preferências do usuário do aplicativo e assim, sempre use o mesmo arquivo de dados -- mesmo que o arquivo de dados seja renomeado, porque o último arquivo usado para o aplicativo é aberto.

Por conseguinte, a 4D permite ligar o caminho do arquivo de dados ao caminho da aplicação. Neste caso, o arquivo de dados será vinculado usando um caminho específico e não será apenas o último arquivo aberto. Assim, você vincula seus dados **pelo caminho da aplicação**.

Este modo permite a você duplicar seus aplicativos mesclados sem quebrar o link para o arquivo de dados. No entanto, com esta opção, se o pacote do aplicativo for movido no disco, o usuário será solicitado por um arquivo de dados, já que o caminho do aplicativo não corresponderá mais ao atributo "executablePath" (depois que um usuário tenha selecionado um arquivo de dados, o *lastDataPath. ml* arquivo é atualizado adequadamente).

*Duplicação quando os dados são vinculados pelo nome da aplicação:* ![](../assets/en/Project/datalinking1.png)

*Duplicação quando os dados estiverem ligados por caminho da aplicação:* ![](../assets/en/Project/datalinking2.png)

Você pode selecionar o modo de ligação de dados durante o processo de construção do aplicativo. Você também pode:

* Use a [página Aplicação](#application-page) ou [Cliente/Página do servidor](#clientserver-page) da caixa de diálogo Construção de aplicações.
* Use a chave **LastDataPathLookup** XML (aplicativo de usuário único ou aplicativo do servidor).

### Definição de uma pasta de dados por defeito

4D permite definir um ficheiro de dados padrão na fase de construção da aplicação. Quando a aplicação é iniciada pela primeira vez, se nenhum arquivo de dados local for encontrado (veja [abertura sequencia descrita acima do](#opening-the-data-file)), o arquivo de dados padrão é aberto automaticamente no modo somente leitura por 4D. Isto dá a você melhor controle sobre a criação e/ou abertura de arquivos ao iniciar uma aplicação mesclada pela primeira vez.

Mais especificamente, são abrangidos os seguintes casos:

* Evitar a exibição da caixa de diálogo 4D "Abrir Arquivo de Dados" ao iniciar um aplicativo novo ou atualizado com mesclagem. Você pode detectar, por exemplo, na inicialização, que o arquivo de dados padrão foi aberto e, portanto, executa seu próprio código e/ou diálogos para criar ou selecionar um arquivo de dados local.
* Permitir a distribuição de aplicativos mesclados com dados somente de leitura (para aplicativos de demonstração, por exemplo).

Para definir e utilizar um ficheiro de dados padrão:

* Você fornece um arquivo de dados padrão (chamado "Default.4DD") e o armazena em uma pasta padrão (chamado "Dados Padrão") dentro da pasta do projeto do aplicativo. Este arquivo deve ser fornecido juntamente com todos os outros arquivos necessários, dependendo da configuração do projeto: índice (.4DIndx), Blobs externos, periódico, etc. É sua responsabilidade fornecer um ficheiro de dados padrão válido. É sua responsabilidade fornecer um ficheiro de dados padrão válido. No entanto, note que, uma vez que um arquivo de dados padrão é aberto em modo somente leitura, é recomendável desmarcar a opção "Usar Arquivo de Log" no arquivo de estrutura original antes de criar o arquivo de dados.
* Quando a aplicação é criada, a pasta de dados predefinida é integrada na aplicação fundida. Todos os ficheiros dentro desta pasta de dados predefinida também são incorporados.

O gráfico seguinte ilustra esta funcionalidade:

![](../assets/en/Project/DefaultData.png)

Quando o arquivo de dados padrão é detectado na primeira inicialização, ele é silenciosamente aberto em modo somente leitura Assim, permite que você execute operações personalizadas que não modifiquem o arquivo de dados em si.

## Gestão da(s) ligação(ões) cliente

A gestão de conexões por aplicativos cliente cobre os mecanismos pelos quais um aplicativo cliente mesclado se conecta ao servidor de destino, uma vez situada no seu ambiente de produção.

### Cenário de ligação

O procedimento de conexão para aplicativos cliente mesclados suporta casos onde o servidor dedicado não está disponível. O cenário de inicialização de um aplicação cliente 4D é o seguinte:

* A aplicaçao cliente tenta se conectar ao servidor usando o serviço de descoberta (baseado no nome do servidor, transmitido na mesma subnet).  
  OU  
  Se informações válidas de conexão forem armazenadas no "EnginedServer. Arquivo DLink" dentro da aplicaçao cliente, a aplicaçao cliente tenta se conectar ao endereço especificado do servidor.
* Se isso falhar, o aplicativo cliente tenta se conectar ao servidor usando informações armazenadas na pasta de preferências do usuário do aplicativo ("lastServer. ml" arquivo, veja a última etapa).
* Se isso falhar, o aplicativo cliente exibe uma caixa de diálogo de erro de conexão.
  * Se o usuário clicar no **Select... Botão** (quando permitido pelo desenvolvedor 4D na etapa de compilação, veja abaixo), a caixa de diálogo padrão "conexão do servidor" é exibida.
  * Se o usuário clica no botão **Sair** , o aplicativo será encerrado.
* Se a conexão for bem-sucedida, o aplicativo cliente salva esta informação de conexão na pasta de preferências de usuário do aplicativo para uso futuro.

### Armazenar o último caminho do servidor

O último caminho de servidor usado e validado é automaticamente salvo em um arquivo chamado "lastServer.xml" na pasta de preferências do usuário do aplicativo. Esta pasta está armazenada na seguinte localização:

```4d
userPrefs:=Get 4D folder(Pasta 4D activa)
```

Este mecanismo aborda o caso de o servidor principal alvo estar temporariamente indisponível por algum motivo (modo de manutenção, por exemplo). Quando este caso ocorre pela primeira vez, a caixa de diálogo de seleção do servidor é exibida (se permitido, veja abaixo) e o usuário pode selecionar manualmente um servidor alternativo, cujo caminho é então salvo se a conexão for bem-sucedida. Qualquer não-disponibilidade subsequente seria tratada automaticamente através da informação do caminho "lastServer.xml".

> * Quando aplicativos do cliente não podem se beneficiar permanentemente do serviço de descoberta, por exemplo, por causa da configuração de rede, é recomendável que o desenvolvedor forneça um nome de host no momento da build usando a chave [IP](https://doc.4d.com/4Dv17R6/4D/17-R6/IPAddress.300-4465710.en.html) do "BuildApp. Arquivo DConfigurações" O mecanismo aborda os casos de indisponibilidade temporária.  
> * Pressionando a tecla **Al/Opção** na inicialização para exibir a caixa de diálogo de seleção do servidor ainda é suportada em todos os casos.

### Disponibilidade da caixa de diálogo de seleção do servidor em caso de erro

Você pode escolher se deseja ou não exibir a caixa de diálogo de seleção padrão do servidor em aplicações cliente mescladas quando o servidor não pode ser alcançado. A configuração depende do valor da chave XML [ServerSelectionAllowed](https://doc.4d.com/4Dv17R6/4D/17-R6/ServerSelectionAllowed.300-4465714.en.html) no computador em que a aplicação foi criada:

* **exibir uma mensagem de erro sem acesso possível à caixa de diálogo de seleção do servidor**. Operação padrão. O aplicativo só pode sair.  
  `ServerSelectionAllowed`: **False** ou key omitida ![](../assets/en/Project/connect1.png)

* **exibir uma mensagem de erro com acesso à caixa de diálogo de seleção do servidor possível**. O usuário pode acessar a janela de seleção do servidor clicando no botão **Selecionar...**. `ServerSelectionAllowed`: **True** ![](../assets/en/Project/connect2.png) ![](../assets/en/Project/connect3.png)
