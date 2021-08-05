# desafio03-ignite-reactjs

## Criando uma aplicação de um blog do zero com Prismic CMS a partir de um layout do Figma.


### Sobre o desafio

Nesse desafio, você deverá criar uma aplicação para treinar o que aprendeu até agora no ReactJS

Essa será uma aplicação onde o seu principal objetivo é criar um blog do zero. Você vai receber uma aplicação praticamente em branco que deve consumir os dados do Prismic e ter a interface implementada conforme o layout do Figma. Você terá acesso a diversos arquivos para implementar:

- Estilizações global, comun e individuais;
- Importação de fontes Google;
- Paginação de posts;
- Cálculo de tempo estimado de leitura do post;
- Geração de páginas estáticas com os métodos `getStaticProps` e `getStaticPaths`;
- Formatação de datas com `date-fns`;
- Uso de ícones com `react-icons`;
- Requisições HTTP com `fetch`;
- Entre outros.

A seguir veremos com mais detalhes o que e como precisa ser feito 🚀

### Prismic

Como você já deve ter visto nas aulas, o Prismic é uma Headless CMS. Vamos utilizá-lo para gerar documentos repetíveis (post) que vão retornar alguns dados para a aplicação. Nesse ponto, é muito importante que você siga exatamente a estrutura que vai ser apresentada aqui pois os testes dependem disso.

- **slug**
    - Tipo: UID
    - Descrição: Identificador único amigável de cada post. Pode receber um valor manualmente ou é gerado automaticamente a partir do primeiro campo de texto preenchido. Esse campo vai ser utilizado na navegação do Next.
- **title**
    - Tipo: Key Text
    - Descrição: Input de strings. Recebe valores manualmente. Esse campo será utilizado como título do Post.
- **subtitle**
    - Tipo: Key Text
    - Descrição: Input de strings. Recebe valores manualmente. Esse campo será utilizado como subtítulo do Post.
- **author**
    - Tipo: Key Text
    - Descrição: Input de strings. Recebe valores manualmente. Esse campo será utilizado como nome do autor do Post.
- **banner**
    - Tipo: Image
    - Descrição: Input de imagens. Recebe valores manualmente. Esse campo será utilizado como banner do Post.
- **content**
    - Tipo: Group
    - Descrição: Grupo de campos repetíveis. Esse campo será utilizado como o conteúdo do Post. O conteúdo será dividido em seções com um campo `heading` e um campo `body`.
    - Campos internos:
        - **heading**
            - Tipo: Key Text
            - Descrição: Input de strings. Recebe valores manualmente. Esse campo será utilizado como título da seção do Post.
        - **body**
            - Tipo: Rich Text      
            - Descrição: Input de *rich text* (HTML). Recebe valores manualmente. Esse campo será utilizado como conteúdo da seção do Post. Perceba que nas configurações do campo, selecionamos algumas opções para que o seu texto tenha varias formatações (negrito, hyperlinks, listas, etc.).

Por fim, vamos falar rapidamente dos métodos que esperamos que você utilize em cada arquivo:

- **src/pages/index.tsx**: Utilizar o método `query` para retornar todos os `posts` já com paginação. Por padrão, a paginação vem configurada como 20. Portanto se quiser testar sem ter que criar mais de 20 posts, altere a opção `pageSize` para o valor que deseja.
- **src/pages/posts/[slug.tsx]**: Utilizar o método `query` para buscar todos os `posts` e o `getByUID` para buscar as informações do `post` específico.

Além disso, não esqueça de configurar no arquivo `.env.local` na raiz do seu projeto a variável `PRISMIC_API_ENDPOINT` com a url da sua API

Caso tenha dúvidas, dê uma olhada na documentação oficial do Prismic:

[Prismic w/ Javascript - Prismic](https://prismic.io/docs/technologies/javascript)

[Next.js & Prismic](https://prismic.io/docs/technologies/getting-started-nextjs)

[Prismic Help Center](https://intercom.help/prismicio/en/)

![image](https://user-images.githubusercontent.com/74268252/128435243-1078133c-f276-4bdd-8663-e892a5bf8f85.png)

### Figma

Um ponto muito importante desse desafio que queremos que vocês exercitem é a implementação de uma interface a partir de um layout do Figma, como se você tivesse recebido isso das mãos de um designer.

Nesse desafio, você deve implementar o layout da página `Obrigatório`.

Para utilizar o Figma, não possui muito mistério. Vamos deixar abaixo os passos para criar uma conta, duplicar o layout e exportar imagens.

### Criando uma conta no Figma

Para acessar o Layout da aplicação, você primeiramente deve ter uma conta criada na plataforma do Figma, para isso, você pode [clicar aqui](https://www.figma.com/signup). 

Então, na página de cadastro, você pode logar diretamente com sua conta do Google ou criar uma conta com o e-mail que você preferir.

### Utilizando o Figma

Após criar sua conta, você pode acessar sua Dashboard do Figma, para isso, basta acessar [https://www.figma.com/](https://www.figma.com/) e ele vai te redirecionar para a Dashboard.

Caso ele não redirecione diretamente para a sua dashboard, existe um botão "Log in" no canto superior direito da tela, que permitirá você acessar a conta que você acabou de criar e, ao logar, você será redirecionado automaticamente.

### Acessando o layout do app

Agora para duplicar os layouts, basta você clicar no link abaixo. Ele adicionará o Layout à sua dashboard do Figma automaticamente, como uma cópia.

[Desafios Módulo 3 ReactJS](https://www.figma.com/file/0Y26j0tf1K2WB5c1ja5hov/Desafios-M%C3%B3dulo-3-ReactJS/duplicate)

### Verificando estilização

Para verificar a estilização de um elemento, basta selecioná-lo e escolhar na barra lateral direito a opção `Inspect` no menu superior direito. Dessa forma você vai ter a maioria das informações que precisa. Caso precise das distâncias em relação a outros elementos, basta colocar o mouse em cima do elemento que deseja pegar a distância.
### Exportando do Figma

Se você está tendo dificuldades em encontrar o comando `Export` no layout do Figma, siga esses passos:

- Selecione o item que deseja exportar;
- Na sidebar direita, clique na aba `Design`;
- Deslize até o final da sidebar para encontrar a opção `Export`.

### Fetch

Para que você consiga realizar a paginação, é preciso trabalhar com a propriedade `next_page` retornada no método `query`. Ela retorna um link que vai buscar a próxima página da paginação. 

Dessa forma, para realizar essa única requisição no seu projeto, é **obrigatório** que você utilize o `fetch` já disponível de forma global.

Caso tenha dúvidas de como utilizar, o Diego utilizou o `fetch` no primeiro módulo, lá dentro do `RepositoryList.tsx`. Deixaremos abaixo também a documentação oficial

[Usando Fetch](https://developer.mozilla.org/pt-BR/docs/Web/API/Fetch_API/Using_Fetch)

## React-icons

Para exibir os ícones de data de criação, tempo estimado de leitura e autor do post sugerimos utilizar a lib `react-icons` já instalada no seu template. Todos os três icones são da coleção `Feather Icons`. 

Caso tenha dúvidas de como utilizar, dê uma olhada na documentação oficial.

[React Icons](https://react-icons.github.io/react-icons/)

### Date-fns

Para realizar a formatação das datas, sugerimos utilizar a lib `date-fns` já instalada no seu template. O único método que você precisa utilizar é o `format` informando o `locale` como `pt-BR`. Segue abaixo um rápido exemplo:

```tsx
import { format } from 'date-fns';
import ptBR from 'date-fns/locale/pt-BR';

format(
	new Date(),
	"'Hoje é' eeee",
	{
		locale: ptBR,
	}
)
```

Caso tenha dúvidas de como utilizar, dê uma olhada na documentação oficial.

[Modern JavaScript Date Utility Library](https://date-fns.org/docs/Getting-Started)

![image](https://user-images.githubusercontent.com/74268252/128435035-7abe5880-b4cf-4f1d-afd7-6dacb832e063.png)
![image](https://user-images.githubusercontent.com/74268252/128435065-98cf2ca0-d94b-46aa-a70d-d3c4eaca2953.png)
![image](https://user-images.githubusercontent.com/74268252/128435090-2b63ed60-94be-4679-86c5-dc74a1428e2b.png)



