<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Grade Escolar Noturna</title>

<style>
body {
    font-family: 'Segoe UI', sans-serif;
    background: linear-gradient(135deg, #1e3c72, #2a5298);
    color: white;
    margin: 0;
    padding: 20px;
}

h1 {
    text-align: center;
}

.container {
    max-width: 1400px;
    margin: auto;
}

.controls {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    margin-bottom: 20px;
}

select {
    padding: 10px;
    border-radius: 8px;
    border: none;
    margin: 5px;
}

table {
    width: 100%;
    border-collapse: collapse;
    background: white;
    color: black;
    border-radius: 10px;
    overflow: hidden;
}

th {
    background: #222;
    color: white;
}

th, td {
    padding: 10px;
    text-align: center;
}

/* cores */
.matematica { background: #75c1ff; }
.portugues { background: #ff7474; }
.historia { background: #ffeaa7; }
.geografia { background: #557eef; }
.fisica { background: #a59bfe; }
.quimica { background: #79fd8b; }
.biologia { background: #81e8ec; }
.ingles { background: #c1c9a6; }
.filosofia { background: #8a9397; }
.intervalo { background: #636e72; color: white; }
</style>
</head>

<body>

<div class="container">
<h1>📚 Grade Escolar Noturna</h1>

<div class="controls">
    <select id="dia" onchange="mostrarAulas()">
        <option value="segunda">Segunda</option>
        <option value="terca">Terça</option>
        <option value="quarta">Quarta</option>
        <option value="quinta">Quinta</option>
        <option value="sexta">Sexta</option>
    </select>

    <select id="turma" onchange="mostrarAulas()">
        <option value="todas">Todas</option>
        <option value="0">1EI</option>
        <option value="1">2EI</option>
        <option value="2">3EI</option>
        <option value="3">1DDA</option>
        <option value="4">2DDS</option>
        <option value="5">3DDS</option>
        <option value="6">1ASA</option>
        <option value="7">2ASA</option>
        <option value="8">3D</option>
    </select>
</div>

<table>
<thead>
<tr>
    <th>Horário</th>
    <th>1EI</th>
    <th>2EI</th>
    <th>3EI</th>
    <th>1DDA</th>
    <th>2DDS</th>
    <th>3DDS</th>
    <th>1ASA</th>
    <th>2ASA</th>
    <th>3D</th>
</tr>
</thead>
<tbody id="tabela"></tbody>
</table>

</div>

<script>
const horarios = [
    "18:45 - 19:30",
    "19:30 - 20:15",
    "20:15 - 21:00",
    "21:00 - 21:15",
    "21:15 - 22:00",
    "22:00 - 22:45"
];

const materias = ["matematica","portugues","historia","geografia","fisica","quimica","biologia","ingles","filosofia"];

function randomMateria() {
    return materias[Math.floor(Math.random() * materias.length)];
}

/* gera grade automática */
const grade = {};
["segunda","terca","quarta","quinta","sexta"].forEach(dia => {
    grade[dia] = [];
    for(let i=0;i<6;i++){
        let linha = [];
        for(let t=0;t<9;t++){
            if(i===3) linha.push("intervalo");
            else linha.push(randomMateria());
        }
        grade[dia].push(linha);
    }
});

const nomes = {
    matematica:"Matemática",
    portugues:"Português",
    historia:"História",
    geografia:"Geografia",
    fisica:"Física",
    quimica:"Química",
    biologia:"Biologia",
    ingles:"Inglês",
    filosofia:"Filosofia",
    intervalo:"Intervalo"
};

function mostrarAulas() {
    const dia = document.getElementById("dia").value;
    const turma = document.getElementById("turma").value;
    const tabela = document.getElementById("tabela");

    tabela.innerHTML = "";

    grade[dia].forEach((aula, i) => {
        let linha = "<tr>";
        linha += `<td>${horarios[i]}</td>`;

        aula.forEach((m, index) => {
            if (turma === "todas" || turma == index) {
                linha += `<td class="${m}">${nomes[m]}</td>`;
            } else {
                linha += `<td>-</td>`;
            }
        });

        linha += "</tr>";
        tabela.innerHTML += linha;
    });
}

mostrarAulas();
</script>

</body>
</html>
