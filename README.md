## Evento EBAC - 24/02/25
# Java com Spring Boot: Criando Aplicações Robustas com Abordagem Prática


A base do projeto foi realizada com o [start.spring.io](https://start.spring.io/) com as configurações abaixo:
- Project: Maven
- Language: Java
- Spring Boot: 3.4.3
- Project Metadata: conforme a imagem (_este pode variar de acordo com sua vontade_)
- Packagiing: Jar
- Java: 17
- Dependencies: _iniciamos sem nada personalizado, mas pode verificar de já trazer o Spring Batch_

![image](https://github.com/user-attachments/assets/3d73a78e-964c-4148-87da-5b693a3a08a1)


O projeto é um exemplo básico de uma solução básica baseada em lote (batch).

Os pacotes do projeto são:

📂 ebac
├── 📂 src
│   ├── 📂 main
│   │   ├── 📂 java/com/example/ebac
│   │   │   ├── 📄 FileProcessingInJavaApplication.java  # Classe principal (@SpringBootApplication)
│   │   │   ├── 📂 config
│   │   │   │   ├── 📄 BatchConfiguration.java  # Classes de configuração (@Configuration)
│   │   │   ├── 📂 listener
│   │   │   │   ├── 📄 JobCompletionNotificationListener.java  # Componentes (@Component)
│   │   │   ├── 📂 model
│   │   │   │   ├── 📄 MeuRepository.java  # Interface para acesso a dados
│   │   │   ├── 📂 model
│   │   │   │   ├── 📄 Person.java  # Representação de entidades
│   │   │   ├── 📂 processor
│   │   │   │   ├── 📄 PersonItemProcessor.java  # Regras de processamento
│   │   ├── 📂 resources
│   │   │   ├── 📄 application.properties  # Configurações do projeto
│   │   │   ├── 📄 sample-data.csv  # Arquivo de exemplo do projeto
│   │   │   ├── 📄 schema-all.sql  # Scripts SQL
│   │   │   ├── 📂 static/  # Arquivos estáticos (**se aplicável**)
│   │   │   ├── 📂 templates/  # Templates para renderização (**se aplicável**)
│   ├── 📂 test
│   │   ├── 📂 java/com/example/ebac
│   │   │   ├── 📄 FileProcessingInJavaApplicationTests.java  # Testes unitários (@SpringBootTest)
├── 📄 pom.xml  # Arquivo de dependências (Maven)
├── 📄 README.md  # Documentação do projeto

Esse exemplo prevê uma situação que simula o processamento de arquivos utilizando o Spring.
Normalmente, um analista de negócios fornece uma planilha. Para este exemplo simples, criamos um arquivo de CSV para
simular o caso.

Esta planilha contém um nome e um sobrenome em cada linha, separados por uma vírgula.
Este é um padrão bastante comum que o Spring pode manipular sem personalização.

Em seguida, você precisa escrever um script SQL para criar uma tabela para armazenar os dados.

Para salvar essa representação, precisamos da representação dessa entidade, por isso a classe de modelo _Person.java_.
Cada registro de _Person_ pode ser instanciado por meio de um construtor.

Depois, precisamos de um processador intermediário.
Um paradigma comum no processamento em lote (_batch_) é:

1. ingerir dados,
2. transformá-los e,
3. em seguida, canalizá-los para outro lugar.
 
Nosso processador, converte os nomes em letras maiúsculas (_PersonItemProcessor.java_).
_PersonItemProcessor_ implementa a interface _ItemProcessor_ do Spring Batch.

Após criar o processador, você precisa configurar o *batch*.
O Spring Batch fornece muitas classes de utilitários que reduzem a necessidade de escrever código personalizado.
Em vez disso, você pode se concentrar na lógica de negócios (_BatchConfiguration.java_).

O último detalhe da configuração do lote é uma maneira de ser notificado quando o trabalho for concluído (_JobCompletionNotificationListener.java_).

Por último, mas não menos importante, lembre-se de garantir que o projeto é executável.

A abordagem mais simples empacota tudo em um único arquivo JAR executável, controlado por um bom e velho método Java main().


Parabéns! Você criou um trabalho em lote que ingeriu dados de uma planilha, processou-os e os gravou num banco de dados.