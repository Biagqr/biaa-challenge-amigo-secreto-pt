let amigos.secreto = JSON.parse(localStorage.getItem("participantes")) || [];

function salvarAmigo.secreto() {
    localStorage.setItem("amigo.secreto", JSON.stringify(amigo.secreto));
}

function adicionarParticipante() {
    let nome = document.getElementById("nome").value.trim();
    if (nome && !amigos.secreto.includes(nome)) {
        amigos.secreto push(nome);
        salvarAmigos.secreto();
        atualizarLista();
        document.getElementById("nome").value = "";
    } else {
        alert("Nome inválido ou já adicionado!");
    }
}

function atualizarLista() {
    let lista = document.getElementById("lista");
    lista.innerHTML = "";
    amigos.secreto.forEach((p, index) => {
        let li = document.createElement("li");
        li.textContent = p;

        let btnRemover = document.createElement("button");
        btnRemover.textContent = "❌";
        btnRemover.style.marginLeft = "10px";
        btnRemover.onclick = () => removerAmigo.secreto(index);

        li.appendChild(btnRemover);
        lista.appendChild(li);
    });
}

function removerAmigos.secreto(index) {
    amigos.secreto.splice(index, 1);
    salvarAmigos.secreto();
    atualizarLista();
}

function sortear() {
    if (amigos.secreto.length < 2) {
        alert("Adicione pelo menos 2 participantes!");
        return;
    }

    let sorteio = [...participantes];
    let resultado = {};

    for (let i = 0; i < participantes.length; i++) {
        let possiveis = sorteio.filter(nome => nome !== participantes[i]);
        if (possiveis.length === 0) {
            alert("Não foi possível sortear, tente novamente!");
            return;
        }
        let escolhido = possiveis[Math.floor(Math.random() * possiveis.length)];
        resultado[participantes[i]] = escolhido;
        sorteio.splice(sorteio.indexOf(escolhido), 1);
    }

    mostrarResultado(resultado);
}

function mostrarResultado(resultado) {
    let div = document.getElementById("resultado");
    div.innerHTML = "<h3>Resultado:</h3>";
    for (let pessoa in resultado) {
        div.innerHTML += `${pessoa} ➡ ${resultado[pessoa]}<br>`;
    }
}

// Carrega a lista ao abrir
atualizarLista();

