$(document).ready(function() {
    // Quando o usuário sair do campo de CEP
    $('#cep').on('blur', function() {
      // Remove caracteres não numéricos do CEP
      var cep = $(this).val().replace(/\D/g, '');
      // Se o CEP não tiver 8 dígitos, exibe um alerta
      if (cep.length != 8) {
        alert('CEP inválido');
        return false;
      }
      // Faz a requisição HTTP para a API ViaCEP
      $.getJSON('https://viacep.com.br/ws/' + cep + '/json/', function(data) {
        // Se a requisição retornar algum erro, exibe um alerta
        if (data.erro) {
          alert('CEP não encontrado');
          return false;
        }
        // Preenche os campos de cidade e estado com os dados da resposta
        $('#inputCidade').val(data.localidade);
        $('#inputEstado').val(data.uf);
      });
    });
  });
  
  // seleciona o campo de CEP
const cepInput = document.querySelector('#cep');

// adiciona um event listener para o evento "blur" que é disparado quando o campo perde o foco
cepInput.addEventListener('blur', () => {
  // remove a classe de erro caso exista
  cepInput.classList.remove('error');

  // remove a mensagem de erro caso exista
  const errorMessage = cepInput.nextElementSibling;
  if (errorMessage && errorMessage.classList.contains('error-message')) {
    errorMessage.remove();
  }

  // verifica se o valor do campo de CEP é válido
  const cepValue = cepInput.value;
  if (!/^\d{5}-?\d{3}$/.test(cepValue)) {
    // adiciona a classe de erro
    cepInput.classList.add('error');

    // cria a mensagem de erro e adiciona a classe de erro-message
    const errorMessage = document.createElement('div');
    errorMessage.innerText = 'CEP inválido';
    errorMessage.classList.add('error-message');

    // insere a mensagem de erro após o campo de CEP
    cepInput.insertAdjacentElement('afterend', errorMessage);
  }
});

// Seleciona o botão "Ver crachá virtual"
var verCrachaBtn = document.getElementById('btn-ver-crachá');



// Adiciona um ouvinte de evento ao clicar no botão "Ver crachá virtual"
verCrachaBtn.addEventListener('click', function() {
var imgCracha = document.getElementById('cracha-virtual');
// Exibe a imagem do crachá virtual
imgCracha.style.display = 'block';
 
  // Seleciona todos os campos do formulário
  var dadosformulario = document.getElementById('dados-formulario');
  var apelido = document.getElementById('inputApelido').value;
  var nome = document.getElementById('inputNome').value;
  console.log(nome); // verificar se o valor é o esperado
  var cidade = document.getElementById('inputCidade').value;
  console.log(cidade); // verificar se o valor é o esperado
  var estado = document.getElementById('inputEstado').value;
  console.log(estado); // verificar se o valor é o esperado
  var telefone = document.getElementById('inputTelefone').value;
  console.log(telefone); // verificar se o valor é o esperado
  var categoriaUsuario = document.getElementById('selectCategoriaUsuario').value;
  var tipoUsuario = document.getElementById('tipo-usuario').value;
  var status = document.getElementById('status').value;
  var formaçãoum = document.getElementById('formaçãoum').value;
  var forma = document.getElementById('forma').value;
  
   // Mostra o crachá e o botão "Finalizar cadastro"
  
  document.querySelector('.crachá-container').style.display = 'block';
  document.querySelector('#btn-finalizar-cadastro').style.display = 'block';
  document.querySelector('#dados-formulario').style.display = 'block';
  

  // Atualiza o texto dos elementos de exibição dos dados do formulário
  let telefoneFormatado = telefone.replace(/(\d{2})(\d{5})(\d{4})/, "$1 ***** $3");
dadosformulario.innerHTML =`
  
  <!-- Adiciona a classe nome-apelido ao elemento HTML que contém ${apelido} -->
<p class="nome-apelido" style="font-weight:bold; font-size: 16px;"><strong></strong><span class="espaco-rigth"> </span>${apelido}</p>

  <br>
  <br>
  <p><strong>Nome:</strong> ${nome}</p>
  <p><strong>Cidade-UF:</strong> ${cidade} - ${estado}</p>
  <p><strong>Telefone:</strong> ${telefoneFormatado}</p>
  <p><strong>Categoria Usuário:</strong> ${categoriaUsuario}</p>
  <p><strong>Tipo de Usuário:</strong> ${tipoUsuario}</p>
  <p><strong>Profissão:</strong> ${status}</p>
  <p><strong>Formação</strong> ${formaçãoum}</p>
  <p><strong>      </strong> ${forma}</p>
`;

 

  // Muda o texto do botão para "Fechar crachá virtual"
  verCrachaBtn.textContent = 'Fechar crachá virtual';
  

});


  // Adiciona um novo ouvinte de evento para o botão "Fechar crachá virtual"
verCrachaBtn.addEventListener('click', function closeCracha() {
// Esconde o crachá, informações do formulário e botão "Finalizar cadastro"
document.querySelector('.crachá-container').style.display = 'none';
document.querySelector('#btn-finalizar-cadastro').style.display = 'none';


// Muda o texto do botão para "Ver crachá virtual"
verCrachaBtn.textContent = 'Ver crachá virtual';

// Remove o ouvinte de evento "closeCracha" do botão "Fechar crachá virtual"
verCrachaBtn.removeEventListener('click', closeCracha);

// Adiciona um novo ouvinte de evento para o botão "Ver crachá virtual"
verCrachaBtn.addEventListener('click', function() {
  // Mostra o crachá e o botão "Finalizar cadastro"
  document.querySelector('.crachá-container').style.display = 'block';
  document.querySelector('#btn-finalizar-cadastro').style.display = 'block';

  // Muda o texto do botão para "Fechar crachá virtual"
  verCrachaBtn.textContent = 'Fechar crachá virtual';

  // Remove o ouvinte de evento do botão "Ver crachá virtual"
  verCrachaBtn.removeEventListener('click', arguments.callee);

  // Adiciona um novo ouvinte de evento para o botão "Fechar crachá virtual"
  verCrachaBtn.addEventListener('click', closeCracha);
});
});

const imagemPerfil = document.querySelector('#imagem-perfil');
const fotoContainer = document.querySelector('.classe-do-avatar');


imagemPerfil.addEventListener('change', function(event) {
  fotoContainer.style.display = 'block';
  const file = event.target.files[0];

  

  // Cria um objeto FileReader
  const reader = new FileReader();

  // Defina uma função de callback para quando a imagem for carregada
  reader.onload = function(e) {
    // Crie um elemento de imagem e defina seu atributo src como a imagem carregada
    const img = document.createElement('img');
    img.src = e.target.result;

    // Adicione a imagem ao crachá
    const fotoContainer = document.getElementById('cracha-virtual');
    fotoContainer.innerHTML = '';
    fotoContainer.appendChild(img);
  }

  // Leia o conteúdo da imagem como uma URL de dados
  reader.readAsDataURL(file);
});

$(document).ready(function() {
  $('#meu-formulario').submit(function(event) {
    event.preventDefault(); // evita que a página seja recarregada
    var dados = $(this).serialize(); // serializa os dados do formulário para enviar por HTTP POST
    $.post('/ProcessaCadastro', dados, function(resposta) {
      alert('Dados inseridos com sucesso!');
    });
  });
});
