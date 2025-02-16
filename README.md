### Inicial
Agora vamos testar nossos work flows em uma aplicação react 

tipos de eventos 
- push 
- pull_request
- creat 
- fork
- issues 
- issue_comment
- watch 
- discussion 

E muito mais 

<p> Podemos usar actions que são ações comuns como baixar o código  </p>
<p> https://github.com/marketplace/actions/checkout </p>
<p> https://github.com/marketplace?type=actions </p>
Para utilizar uma action não um shell use <br>
<p>uses: actions/checkout@v4</p>

#### Multiple jobs 
```yml
name: Test Work Flow
on: push 
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Get the code
        uses: actions/checkout@v4
      - name: Install Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci      
      - name: Run tests
        run: npm test
  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Get the code
        uses: actions/checkout@v4
      - name: Install Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
      - name: Install dependencies
        run: npm ci      
      - name: Build Project Deployment 
        run: npm run build
      - name: Deploy to Firebase
        run: echo "Deploying to Firebase"

```
Aqui temos uma execução que depende da outra uma da outra ou seja um CI/CD