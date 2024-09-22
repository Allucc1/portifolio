# portifolio
Atv de portifolio
<!DOCTYPE html>
<html>
<head>
  <title>Sistema de Funcionários</title>
  <style>
    body {
      font-family: sans-serif;
      margin: 0;
      padding: 20px;
    }

    h1 {
      text-align: center;
      margin-bottom: 20px;
    }

    form {
      display: flex;
      flex-direction: column;
      width: 400px;
      margin: 0 auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    label {
      margin-bottom: 5px;
      font-weight: bold;
    }

    input[type="text"],
    input[type="number"] {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 3px;
      margin-bottom: 15px;
    }

    button[type="submit"] {
      background-color: #4CAF50;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 3px;
      cursor: pointer;
    }

    #resultado {
      margin-top: 20px;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 16px;
    }

    #resultado p {
      margin-bottom: 5px;
    }
  </style>
</head>
<body>
  <h1>Sistema de Funcionários</h1>
  <form id="form-funcionario">
    <label for="nome">Nome:</label>
    <input type="text" id="nome" name="nome" required><br><br>
    <label for="idade">Idade:</label>
    <input type="number" id="idade" name="idade" required><br><br>
    <label for="cargo">Cargo:</label>
    <input type="text" id="cargo" name="cargo" required><br><br>
    <label for="departamento">Departamento:</label>
    <input type="text" id="departamento" name="departamento"><br><br>
    <label for="linguagem">Linguagem de Programação:</label>
    <input type="text" id="linguagem" name="linguagem"><br><br>
    <button type="submit">Criar Funcionário</button>
  </form>

  <div id="resultado"></div>

  <script>
    class Funcionario {
      constructor(nome, idade, cargo) {
        if (!nome || !idade || !cargo) {
          throw new Error("Nome, idade e cargo são obrigatórios.");
        }
        this.nome = nome;
        this.idade = idade;
        this.cargo = cargo;
      }

      seApresentar() {
        return `Olá, meu nome é ${this.nome}, tenho ${this.idade} anos e trabalho como ${this.cargo}.`;
      }

      trabalhar() {
        return `${this.nome} está trabalhando como ${this.cargo}.`;
      }
    }

    class Gerente extends Funcionario {
      constructor(nome, idade, cargo, departamento) {
        super(nome, idade, cargo);
        this.departamento = departamento;
      }

      gerenciar() {
        return `${this.nome} está gerenciando o departamento ${this.departamento}.`;
      }
    }

    class Desenvolvedor extends Funcionario {
      constructor(nome, idade, cargo, linguagem) {
        super(nome, idade, cargo);
        this.linguagem = linguagem;
      }

      programar() {
        return `${this.nome} está programando em ${this.linguagem}.`;
      }
    }

    function exibirErro(erro) {
      const resultado = document.getElementById('resultado');
      resultado.innerHTML = `<p style="color: red;">${erro.message}</p>`;
    }

    const formFuncionario = document.getElementById('form-funcionario');
    formFuncionario.addEventListener('submit', (event) => {
      event.preventDefault();

      try {
        const nome = document.getElementById('nome').value;
        const idade = parseInt(document.getElementById('idade').value);
        const cargo = document.getElementById('cargo').value;
        const departamento = document.getElementById('departamento').value;
        const linguagem = document.getElementById('linguagem').value;

        // Verifica se todos os campos obrigatórios estão preenchidos
        if (!nome || !idade || !cargo) {
          throw new Error("Nome, idade e cargo são obrigatórios.");
        }

        let funcionario;
        if (departamento) {
          funcionario = new Gerente(nome, idade, cargo, departamento);
        } else if (linguagem) {
          funcionario = new Desenvolvedor(nome, idade, cargo, linguagem);
        } else {
          funcionario = new Funcionario(nome, idade, cargo);
        }

        const resultado = document.getElementById('resultado');
        resultado.innerHTML = `
          <p>${funcionario.seApresentar()}</p>
          <p>${funcionario.trabalhar()}</p>
          ${departamento ? `<p>${funcionario.gerenciar()}</p>` : ''}
          ${linguagem ? `<p>${funcionario.programar()}</p>` : ''}
        `;

      } catch (error) {
        exibirErro(error);
      }
    });
  </script>
</body>
</html>

