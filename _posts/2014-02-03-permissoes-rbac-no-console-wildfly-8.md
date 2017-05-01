---
id: 374
title: Permissões RBAC no console Wildfly 8
date: 2014-02-03T23:37:56+00:00
author: Claudio Miranda
layout: post
guid: https://secure3117.hostgator.com/~claudius/?p=374
permalink: /2014/02/permissoes-rbac-no-console-wildfly-8/
categories:
  - Java
tags:
  - java
  - jboss
  - wildfly
---
# Acesso controlado por permissões no wildfly 8

No JBoss AS 7 (AS7), o usuário de acesso ao console de administração web (GUI) ou por linha de comando (CLI), possuem acesso completo, como um root, pode fazer todas as tarefas de gerenciamento no servidor de aplicativos, como: deploy/undeploy de aplicações, criação de datasources, iniciar/parar servidores, etc.

A partir de sua adoção, foi verificado a necessidade de controlar as permissões para estas tarefas no AS7, por exemplo, ter um grupo de usuários que só podem fazer deploy/undeploy, outro grupo apenas para monitorar, outro grupo para fazer manutenções de rotina, etc.

Então foi criado o suporte a RBAC (Role Based Access Control) no AS7. De fato, com a mudança de nomes do servidor de aplicativos, o AS7 já não recebe atualizações, agora o nome é Wildfly. Então no wildfly 8, que está na versão release candidate, já suporta o RBAC. É o que vou explicar como ele funciona e como configurar e usar esta funcionalidade no wildfly 8.

O suporte a RBAC está disponível no JBoss EAP 6.2. O nome EAP (Enterprise Application Platform), é o nome comercial do servidor de aplicativos wildfly. Ele possui uma interface GUI para associar os usuários com os papéias, bem como as permissões.

O wildfly contém duas formas de controlar as permissões, pelo mecanismo &#8220;simple&#8221; e &#8220;rbac&#8221;. O padrão habilitado é o &#8220;simple&#8221;.

# Sobre o RBAC

O RBAC possui os seguintes conceitos:

  * Papéis: São os agrupamentos de permissões
  * Dados sensíveis: São as informações como nome de usuário e senha, bem como a configuração do RBAC.
  * Log de auditoria: É o log das operações, gravadas em um arquivo no formato json.
  * Elevação: Um usuário SuperUser pode assumir outro papel para executar operações.

O RBAC contém 7 papéis (roles):

  * Monitor: Permissões: Possui as menores permissões. Pode ler configurações e estado do servidor. Não consegue alterar configurações. Não podem acessar dados sensíveis.
  * Deployer: Permissões: Mesmas permissões do Monitor, e também pode efetuar deploy e undeploy.
  * Operator: Estende o papel monitor. Permissões: Capaz de iniciar/parar um servidor.
  * Maintainer: Permissões: Capaz de modificar as configurações, exceto as informações sensíveis.
  * Administrator: Permissões: Capaz de modificar configurações, incluindo as informações sensíveis. Tem acesso irrestrito, exceto acesar os logs de auditoria.
  * Auditor:  Permissões: Mesmas permissões do Monitor, pode ler (sem modificar) dados sensíveis. Pode ler os logs de auditoria.
  * SuperUser:  Permissões: Possui acesso irrestrito. Pode assumir outro papel sem efetuar logou. É op equivalente de usar o AS7 sem o RBAC.

<a href="https://access.redhat.com/site/documentation/en-US/JBoss_Enterprise_Application_Platform/6.2/html/Administration_and_Configuration_Guide/sect-Securing_the_Management_Interfaces_with_Role-Based_Access_Control.html" target="_blank">Documentação RBAC</a>

<a href="https://access.redhat.com/site/documentation/en-US/JBoss_Enterprise_Application_Platform/6.2/html/Administration_and_Configuration_Guide/sect-Management_Interface_Audit_Logging.html" target="_blank">Documentação sobre log de auditoria</a>

# Adicionar usuários

O RBAC usa os usuários já cadastrados no mgmt-users.properties, portanto é necessário adicionar os usuários.
  
No nosso exemplo, será criado 3 usuários, todos com a mesma senha admin123@

  * admin: super usuário
  * murilo: usuário deployer
  * rafael: usuário maintainer

Vá ao diretório $JB_HOME/bin e reproduza os comandos:

<pre>./add-user.sh -p admin123@ -u admin
./add-user.sh -p admin123@ -u murilo
./add-user.sh -p admin123@ -u rafael</pre>

&nbsp;

# Habilitar o RBAC

Por padrão o wildfly 8 está com o RBAC desabilitado. Para habilitar, pode fazer por CLI ou alterar o arquivo xml. Vou usar o modo domínio nos exemplos.

## Por linha de comando (CLI)

Para usar jboss-cli, conecte com

<pre>$JB_HOME/bin/jboss-cli.sh -c</pre>

Nota2: Quando usa-se o jboss-cli para conectar no mesmo servidor (localhost), a autenticação é do tipo &#8220;local user&#8221; e tem papel de SuperUser (ver item 10.8.3 do guia de administração)

Use o seguinte comando para habilitar o modo RBAC.

<pre>/core-service=management/access=authorization:write-attribute(name=provider,value=rbac)</pre>

É necessário recarregar as configurações:

<pre>reload --host=master</pre>

## Por editar o domain.xml

Nota: Para alterar o arquivo xml, o wildfly deverá estar parado.

Abrir o domain.xml, procurar pelas configurações abaixo e alterar o &#8220;**simple**&#8221; para &#8220;**rbac**&#8221;

<pre>&lt;management&gt;
    &lt;access-control provider="<strong>rbac</strong>"&gt;
        &lt;role-mapping&gt;
            &lt;role name="SuperUser"&gt;
                &lt;include&gt;
                    &lt;user name="$local"/&gt;
                &lt;/include&gt;
            &lt;/role&gt;
        &lt;/role-mapping&gt;
    &lt;/access-control&gt;
&lt;/management&gt;</pre>

# Associar usuários e permissões

Neste momento ao tentar efetuar login na GUI, dará erro: Access denied. Pois nenhum usuário está associado com os papéis.

Então vamos associar o usuário admin com o papel SuperUser. Isso é necessário para o primeiro usuário administrador.

## Por CLI

<pre>/core-service=management/access=authorization/role-mapping=SuperUser/include=user-admin:add(name=admin,type=USER)</pre>

## Ou pelo domain.xml

<pre>&lt;management&gt;
    &lt;access-control provider="rbac"&gt;
        &lt;role-mapping&gt;
            &lt;role name="SuperUser"&gt;
                &lt;include&gt;
                    &lt;user name="$local"/&gt;
                    &lt;user name="admin"/
                &lt;/include&gt;
            &lt;/role&gt;
        &lt;/role-mapping&gt;
    &lt;/access-control&gt;
&lt;/management&gt;</pre>

Inicie o wildfly, acesse o console em <http://localhost:9990> e faça login como admin e navegue até a estrutura Administration.

[<img class="alignnone size-full wp-image-377" alt="rbac1" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac1.png" width="1008" height="515" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac1.png 1008w, http://claudius.com.br/wp-content/uploads/2014/02/rbac1-300x153.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/rbac1-730x372.png 730w" sizes="(max-width: 1008px) 100vw, 1008px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac1.png)

Agora o usuário admin já está pronto para gerenciar outros usuários e permissões.

&nbsp;

# Usar a GUI para associar usuários e permissões

Acesse o endereço <a href="http://localhost:9990" target="_blank"><strong>http://localhost:9990</strong></a> e faça login com o usuário admin.

Veja que existe a aba &#8220;Administration&#8221; que serve para gerenciar a associação de usuários, grupos e papéis.

Nota: O botão de adicionar usuário, é para associar um usuário já existente no mgmt-users.properties com um papel. Ele não cria novos usuários.

A tela de associar usuários, não valida o nome de usuário com o banco de dados de usuários. Sempre confira o nome correto existente no mgmt-users.properties, se o usuário associado não existir, não terá um erro avisando.

Associe o usuário rafael com Maintainer, será usado logo em seguida.
  
Associe o usuário murilo com Deployer.

[<img class="alignnone size-full wp-image-378" alt="rbac2" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac2.png" width="554" height="553" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac2.png 554w, http://claudius.com.br/wp-content/uploads/2014/02/rbac2-150x150.png 150w, http://claudius.com.br/wp-content/uploads/2014/02/rbac2-300x300.png 300w" sizes="(max-width: 554px) 100vw, 554px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac2.png)

&nbsp;

# Teste

Faça logout, efetue login com o usuário rafael.

Navegue na esgrutura Administration, veja que o usuário não possui permissões.

[<img class="alignnone size-full wp-image-380" alt="rbac4" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac4.png" width="656" height="156" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac4.png 656w, http://claudius.com.br/wp-content/uploads/2014/02/rbac4-300x71.png 300w" sizes="(max-width: 656px) 100vw, 656px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac4.png)

&nbsp;

Navegue na estrutura Profiles -> Connector -> Datasource ExampleDS -> Security. Veja que não possui permissão para ver/editar o login/senha.

[<img class="alignnone size-full wp-image-381" alt="rbac5" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac5.png" width="969" height="655" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac5.png 969w, http://claudius.com.br/wp-content/uploads/2014/02/rbac5-300x202.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/rbac5-730x493.png 730w" sizes="(max-width: 969px) 100vw, 969px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac5.png)

&nbsp;

Faça logout, efetue login como murilo.

Navegue nas estruturas Runtime -> Overview. Veja que este usuário não tem permissão para iniciar serviços.

[<img class="alignnone size-full wp-image-382" alt="rbac6" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac6.png" width="985" height="643" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac6.png 985w, http://claudius.com.br/wp-content/uploads/2014/02/rbac6-300x195.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/rbac6-730x476.png 730w" sizes="(max-width: 985px) 100vw, 985px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac6.png)

&nbsp;

Navegue em Profiles -> Datasources, etc. Veja que este usuário não tem permissão para modificar configurações, não há botões Add, Edit, Remove.

[<img class="alignnone size-full wp-image-383" alt="rbac7" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac7.png" width="991" height="702" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac7.png 991w, http://claudius.com.br/wp-content/uploads/2014/02/rbac7-300x212.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/rbac7-730x517.png 730w" sizes="(max-width: 991px) 100vw, 991px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac7.png)

&nbsp;

Este usuário deployer, pode efetuar deploy de aplicações. Habilitar/Desabilitar aplicações.

# Associação de usuário com grupos de servidores ou servidor

É possível associar tarefas administrativas para um grupo de servidores ou um servidor específico.
  
Nos cenários onde um domínio, possui diversos grupos, como: desenvolvimento contabilidade, desenv financeiro, etc.

No nosso exemplo, vamos permitir que o usuário murilo faça deploy apenas no grupo main-server-group.

Logado como admin, navegue na estrutura Administration -> Roles -> Scoped Roles

Adicione uma role, e preencha:

Name: grupo-main-server-group
  
base role: deployer
  
type: server group
  
scope: main-server-group
  
Include all: marcado

Salve.

[<img class="alignnone size-full wp-image-379" alt="rbac3" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac3.png" width="580" height="498" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac3.png 580w, http://claudius.com.br/wp-content/uploads/2014/02/rbac3-300x257.png 300w" sizes="(max-width: 580px) 100vw, 580px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac3.png)

Vá na aba Users, selecione o usuário murilo, clique em Edit.
  
&#8211; na caixa Assigned Roles, clique em Deployer e clique na seta a mover para a caixa Available Roles
  
&#8211; na caixa Available roles, clique em grupo-main-server-group e clique na seta a mover para Assigned Roles, salve.

[<img class="alignnone size-full wp-image-384" alt="rbac8" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac8.png" width="734" height="709" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac8.png 734w, http://claudius.com.br/wp-content/uploads/2014/02/rbac8-300x289.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/rbac8-730x705.png 730w" sizes="(max-width: 734px) 100vw, 734px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac8.png)

&nbsp;

faça logou e login como murilo.

Faça o deploy de um jar qualquer. Ao associar com um grupo de servidores, veja que não é mostrado o grupo other-server-group.

[<img class="alignnone size-full wp-image-385" alt="rbac9" src="https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac9.png" width="771" height="259" srcset="http://claudius.com.br/wp-content/uploads/2014/02/rbac9.png 771w, http://claudius.com.br/wp-content/uploads/2014/02/rbac9-300x100.png 300w, http://claudius.com.br/wp-content/uploads/2014/02/rbac9-730x245.png 730w" sizes="(max-width: 771px) 100vw, 771px" />](https://secure3117.hostgator.com/~claudius/wp-content/uploads/2014/02/rbac9.png)

&nbsp;

# Logs de auditoria

Com diversos usuários acessando e alterando as configurações do servidor, isso é uma certeza de que problemas podem surgir, &#8220;quem fez o deploy ?&#8221;, &#8220;quem removeu o datasource&#8221;, etc. Por isso é necessário manter um log de auditoria das ações dos usuários.

Esse log existe, ele é desabilitado por padrão. O log de auditoria é configurado por host controller ou por servidor. Veja como habilitar.

## com o Wildfly iniciado.

Habilitar o log de auditoria apenas para o host controller.

<pre>/host=master/core-service=management/access=audit/logger=audit-log:write-attribute(name=enabled,value=true)</pre>

&nbsp;

Habilitar o log de auditoria para todo os servidores de um host controller.

<pre>/host=master/core-service=management/access=audit/server-logger=audit-log:write-attribute(name=enabled,value=true)</pre>

&nbsp;

Acima &#8220;master&#8221; é o nome do seu host controller.

## com o wildfly desligado

Abra o host.xml e edite a seção <management> e adicione o <audit-log> como segue

<pre>&lt;management&gt;
    &lt;security-realms&gt;
    ...
    &lt;audit-log&gt;
        &lt;formatters&gt;
            &lt;json-formatter name="json-formatter"/&gt;
        &lt;/formatters&gt;
        &lt;handlers&gt;
            &lt;file-handler name="host-file" formatter="json-formatter" path="audit-log.log" relative-to="jboss.domain.data.dir"/&gt;
            &lt;file-handler name="server-file" formatter="json-formatter" path="audit-log.log" relative-to="jboss.server.data.dir"/&gt;
        &lt;/handlers&gt;
        &lt;logger log-boot="true" log-read-only="false" enabled="true"&gt;
            &lt;handlers&gt;
                &lt;handler name="host-file"/&gt;
            &lt;/handlers&gt;
        &lt;/logger&gt;
        &lt;server-logger log-boot="true" log-read-only="false" enabled="true"&gt;
            &lt;handlers&gt;
                &lt;handler name="server-file"/&gt;
            &lt;/handlers&gt;
        &lt;/server-logger&gt;
    &lt;/audit-log&gt;

    &lt;management-interfaces&gt;
    ....
&lt;/management&gt;</pre>

O log de auditoria não tem relação com o subsistema de log, não é possível criar um handler e relacionar com o log de auditoria.
  
Nesta versão, o formato de saída do log é Json, não tem outro. (ver se existe rfe para outros formatos e configurações)

NOTA: pelo formato ser json, e pela quantidade de operações administrativas no domínio, o arquivo de auditoria pode ficar grande, então pense nisso quando ativar o log de auditoria.

Veja um exemplo do log de auditoria, mostra a adição de uma categoria de log “br.com.teste.empresa” no profile “full” pelo usuário “admin”.

<pre>2014-01-31 22:07:35 - {
    "type" : "core",
    "r/o" : false,
    "booting" : false,
    "version" : "8.0.0.Final-SNAPSHOT",
    "user" : "admin",
    "domainUUID" : null,
    "access" : "HTTP",
    "remote-address" : "127.0.0.1/127.0.0.1",
    "success" : true,
    "ops" : [{
        "address" : [
            {
                "profile" : "full"
            },
            {
                "subsystem" : "logging"
            },
            {
                "logger" : "mne"
            }
        ],
        "operation" : "add",
        "category" : "mne",
        "use-parent-handlers" : true,
        "level" : "FINEST",
        "operation-headers" : {
            "access-mechanism" : "HTTP",
            "domain-uuid" : "6485c914-b071-4c6f-aeac-feac7da0835e",
            "push-to-servers" : null
        }
    }]
}</pre>

O formato json, permite que se use scripts de formatação de saída, caso desejem formatar em colunas por exemplo. Isso fica para outro blog.

# Quando usar controle de permissão

Estas permissões no console só são úteis se o cliente realmente precisa dar acesso a outros usuários e garantir uma segurança de acesso e atividades.

Com o uso do controle de acesso por roles, aumentam as tarefas de administração do servidor, de associação de roles, usuários, grupos, servidores, etc.

&nbsp;