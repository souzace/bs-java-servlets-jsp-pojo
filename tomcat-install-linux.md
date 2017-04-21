Instalação Tomcat linux

1º Faça o Download do binário do Tomcat
Usaremos a versão 5.5.36 como descrito no link:

https://archive.apache.org/dist/tomcat/tomcat-5/v5.5.36/bin/apache-tomcat-5.5.36.tar.gz (Linux)

* Após realizar o download Descompacte o arquivo apache-tomcat-5.5.36.tar.gz

[user@host /home/user/Downloads]$ tar -xvzf apache-tomcat-5.5.36.tar.gz

2º Instalação e Configuração do Tomcat como um Serviço

* Mova a pasta criada apache-tomcat-5.5.36 para dentro da pasta /usr/share (root)

[user@host /home/user/Downloads]$ sudo mv -v apache-tomcat-5.5.36 /usr/share

* Entre na pasta /etc/init.d para criar o script de execução:

[user@host /home/user/Downloads]$ sudo cd /etc/init.d

* Crie um arquivo na pasta /etc/init.d (script para o serviço do tomcat)

[user@host /etc/init.d]$ sudo touch tomcat

* Edite o arquivo tomcat com o editor de sua preferencia, usaremos o vim para este exemplo

[user@host /etc/init.d]$ sudo vim tomcat

* O script a seguir, contém instruções para iniciar, reinicializar ou desligar o serviço do tomcat, de acordo como o comando for chamado, adicione as instruções ao arquivo tomcat da pasta etc/init.d:

#!/bin/bash
# description: Tomcat Start Stop Restart
# processname: tomcat
# chkconfig: 234 20 80
JAVA_HOME=/usr/java/jdk1.7.0_80
export JAVA_HOME
PATH=$JAVA_HOME/bin:$PATH
export PATH
CATALINA_HOME=/usr/share/apache-tomcat-5.5.36

case $1 in
start)
sh $CATALINA_HOME/bin/startup.sh
echo "Incializado"
;;
stop)
sh $CATALINA_HOME/bin/shutdown.sh
echo "Desligado"
;;
restart)
sh $CATALINA_HOME/bin/shutdown.sh
echo "Desligado"
sh $CATALINA_HOME/bin/startup.sh
echo "Inicializado"
;;
esac
exit 0

* Salve, feche o arquivo e em seguida aplique as permissões para tornar o script tomcat em um executável:

[user@host /etc/init.d]$ sudo chmod 755 tomcat

* Use o comando chkconfig para que o tomcat inicie no momento da inicialização do sistema operacional, usaremos níveis de prioridade para inicializar e parar o serviço, você pode ajustar conforme a necessidade:

[user@host /etc/init.d]$ sudo chkconfig --add tomcat
[user@host /etc/init.d]$ sudo --level 234 tomcat on

* Verifique:

[user@host /etc/init.d]$ sudo chkconfig --list tomcat
tomcat          0:off   1:off   2:on    3:on    4:on    5:off   6:off

3º Teste o script

* Comando para inicializar o tomcat (root)
[user@host /etc/init.d]$ sudo service tomcat start

* Veja se a saída está parecida com essa:
Using CATALINA_BASE:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_HOME:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_TMPDIR: /usr/share/apache-tomcat-5.5.36/temp
Using JRE_HOME:        /usr/java/jdk1.7.0_8
Using CLASSPATH:       /usr/share/apache-tomcat-5.5.36/bin/bootstrap.jar
Inicializado

* Comando para desligar o tomcat (root)
[user@host /etc/init.d]$ sudo service tomcat stop
Using CATALINA_BASE:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_HOME:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_TMPDIR: /usr/share/apache-tomcat-5.5.36/temp
Using JRE_HOME:        /usr/java/jdk1.7.0_8
Using CLASSPATH:       /usr/share/apache-tomcat-5.5.36/bin/bootstrap.jar
Desligado

* Comando para reinicializar o tomcat (root)

[user@host /etc/init.d]$ sudo service tomcat restart
Using CATALINA_BASE:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_HOME:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_TMPDIR: /usr/share/apache-tomcat-5.5.36/temp
Using JRE_HOME:        /usr/java/jdk1.7.0_8
Using CLASSPATH:       /usr/share/apache-tomcat-5.5.36/bin/bootstrap.jar
Desligado
Using CATALINA_BASE:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_HOME:   /usr/share/apache-tomcat-5.5.36
Using CATALINA_TMPDIR: /usr/share/apache-tomcat-5.5.36/temp
Using JRE_HOME:        /usr/java/jdk1.7.0_8
Using CLASSPATH:       /usr/share/apache-tomcat-5.5.36/bin/bootstrap.jar
Inicializado

4º Checando os logs e a Página de Gerenciamento do Tomcat

* Para acessar os logs digite o comando abaixo:

[user@host /etc/init.d]$ more /usr/share/apache-tomcat-5.5.36/logs/catalina.out

* Para acessar a página de Gerenciamento do Tomcat pode ser acessado de qualquer brower instalado pelo endereço:
http://localhost:8080/





