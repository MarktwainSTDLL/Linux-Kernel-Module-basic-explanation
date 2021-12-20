# Linux Kernel Module - Part 1

  - Explicação geral de toda estrutura do nosso LKM.

  <img src="https://imgur.com/EOm0gAs.png">
    <b>Bom, temos aqui então todo nosso cabeçalho de includes de bibliotecas. Vamos fazer uma explicação sobre cada biblioteca dessa de uma forma mais completa,
    já que expliquei de forma resumida no projeto.</b>
<br>
<br>
    
<b><h2>📌 -> Linux/Kernel.h</b>:</h2> é o cabeçalho para construção de modulos, é o cabeçalho que faz parte do código-fonte do kernel do linux e é a library que importei para trabalhar com a construção de módulos.

<b><h2>📌 -> Linux/Module.h</b>:</h2> é o cabeçalho que trabalha com modulos do Kernel, é o cabeçalho que nos ajudará na construção do nosso módulo e também faz parte do código-fonte do kernel do linux.

<b><h2>📌 -> Linux/init.h</b>:</h2> é o cabeçalho que trabalha com a inicialização e término de dados como algum dos módulos finais.

  - Setando módulos
  
  <img src="https://imgur.com/HBCuki1.png">
  <b>Aqui setamos alguns módulos como módulos de descrição, autor, licença e até a versão do nosso projeto LKM.</b>
  

# Estrutura geral do LKM

  - Início da classe init_modsys 
  
  <img src="https://imgur.com/umOhUkT.png">
    <b>Aqui vamos falar sobre toda essa estrutura e explicar sobre a diferença entre printk() e printf()</b>
   <br>
   <br>
   
   <b><h2>📌 -> static int __init init_modsys(void)</b>:</h2> Esta é a primeira função que fiz para iniciar o nosso LKM. Essa função é carregada assim que o módulo é executado. Ou seja, o conteúdo que colocamos dentro dela aparecerá dentro dos logs do kernel. Confira abaixo:
   
   <img src="https://imgur.com/0ey3cQO.png">
   <b>O mesmo ocorre quando descarregamos o LKM na nossa função [static int __exit exit_modsys(void)]. Confira abaixo.</b>
   <img src="https://imgur.com/Q4izZbj.png">
   
   <i>Mas daí surge uma dúvida. Como essas mensagens foram chegar ali...?</i>
   
   <b><h2>📌 -> Conhecendo o printk()</b>:</h2>
   
   - Vamos entender como o printk() funciona e qual é a sua diferença com o printf()

  <i>Init function</i>
   <img src="https://imgur.com/jsL2jjh.png">
   <br>
  <i>Exit function</i>
   <img src="https://imgur.com/AAcarmM.png">
   
   
   <h3>🌕<b> Printk() x Printf()</b></h3>
   <br>
    <b>
    🌘 printk() ~# Essa função C da interface do Linux é uma função que imprime mensagens em diferentes níveis de logs do Kernel. Essa função trabalha com um parâmetro denominado
    string de formato, que é um método que renderiza um número arbitrário de tipos de dados variados em uma string e essa string é a string que é impressa no
    log do kernel.
  
    🌒 printf() ~# Essa função C uma das principais funções de output do C. As strings de formato printf são complementares da função de string de formato
    do scanf() que oferecem um input formatado. Resumidamente, essa função imprime uma mensagem ou resultado no seu terminal após ela ter sido executada.
  
    🌗 Diferença entre ambos: Por mais que a função printk() seja baseada no printf(), em algumas situações é impossível usa-la da mesma forma que o printf().
  
      
  <br>Vejamos o motivo:
      <br>
      <br>
  <i>Níveis de registro</i>
  
      ⭐️ A função printk() permite que um chamador especifique o tipo e a importância de uma mensagem que está sendo enviada. Este especificador é chamado
        de nível de log. O nível de registro especifica o tipo de mensagem que está sendo enviada para o registro do Kernel. O nível de kernel é especificado
        prefixando uma string que descreve o nível de log até o início da mensagem ser reproduzida.
  <br>
  <br>
        🪵 Por exemplo: Uma mensagem pode ser reproduzida no KERN_INFO usando a seguinte função em que eu usei no LKM.
        <br>
  <br>
  </b>
      [ printk(KERN_INFO "Estou aqui, amigo :)\n"); ]
      
<b> Mas o que é essa função KERN_INFO? O que ela faz? </b>
  
💥 Bom, aqui contém alguns exemplo de tipos de níveis de registros. <a href="https://elinux.org/Debugging_by_printing#Log_Levels">clique aqui</a><br>
Mas explicando de forma rápida, básicamente é o tipo de Registro de Nível em que queremos que seja enviado para o Kernel.

<h1>Init e Exit Modules</h1>
  - Temos então duas funções simples que estão no final de nosso projeto.
  - Essas funções como já diz, executam uma função do nosso LKM e essa função é a init_modsys e a exit_modsys.

  Exemplificando: <b>Básicamente o sistema vai entender quando é hora de executarmos o nosso LKM e quando é hora de descarregar o Kernel.</b>
  
  - Abaixo estarei deixando os comandos para que você possa executar o LKM em seu sistema. (Recomendo que utilize alguma VM, pois não me responsabilizo por danos causados em sua máquina.)

<h2>🔑 <b> -> Executando o nosso LKM. </b></h2>
  - Primeiro passo é você clonar o Git desse projeto utilizando o seguinte comando: git clone https://github.com/MarktwainSTDLL/Linux-Kernel-Module-basic-explanation.git
  - Segundo passo é você entrar no diretório desse projeto e digitar os seguintes comandos para montarmos o LKM.
    <b>-> make && clear && ls </b><br><br>
  - Você verá que apareceram novos arquivos mas o que devemos nos preocupar é com o file .ko (Kernel Object).
  - digite o seguinte comando: ( insmod kernel_module.ko )

Após ter digitado este comando, você precisa digitar o seguinte comando para ver a mensagem armazenada nos registros do kernel.
  - dmesg
E você vai poder observar que aparecerá uma mensagem bem no final do Registro do Kernel.

  - Mas como eu irei descarregar o Kernel? Bom, digite o seguinte comando: rmmod kernel_module.ko e após isso digite dmesg novamente e você verá que o nosso Registro de Kernel apareceu com outra mensagem, mas foi totalmente descarregado após a execução deste comando.


<h3>Agradeço imensamente a todos por terem lido até aqui e caso vocês encontrarem algum erro aqui, fale comigo pelo discord! É isso ai gente, até o próximo repositório!</h3>

~# Mark desconnected...
  
