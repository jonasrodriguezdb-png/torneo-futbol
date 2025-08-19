<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Fixture Torneo – Fases Finales</title>
<style>
body { font-family: Arial, sans-serif; background:#f9f9f9; margin:20px; }
h1, h2 { text-align:center; }
.day, .fase { margin-bottom:30px; padding:20px; background:white; border-radius:10px; box-shadow:0 2px 5px rgba(0,0,0,0.1);}
.match { margin:10px 0; padding:10px; border:1px solid #ccc; border-radius:8px; background:#f3f3f3; }
.time { font-weight:bold; }
table { width:100%; border-collapse: collapse; margin-top:10px; }
th, td { border:1px solid #ccc; padding:5px; text-align:center; }
input { width:50px; }
</style>
</head>
<body>
<h1>⚽ Fixture Torneo – Fase Regular y Finales</h1>
<div id="fixture"></div>

<script>
const equipos = {
  "La Chispita ⚡️":["Mateo Rezmasud","Matias Pandolfi","Lionel Altamiranda","Benjamin Diaz","Juanfra Ortiz","Gael Ruiz","Joaquin Poggi"],
  "A la Lula":["Maximo Camargo","Ismael Orozco","Joaquin Orihuela","Tiziano Cordi","Santino Carlavan","Urbano De Lucia","Ian Chicala"],
  "La Favorita":["Martino Moyano","Benjamin Rezmasud","Juan Cruz Astesiano","Valentin Nievas","Juan Cruz Gutierrez","Valentino Res Mazmasud","Franco Pons","Santino Morales"],
  "Marcelu FC":["Nicolás Tabanez","Juan Martin Aguirre","David Mamani","Bautista Adell","Luciano Oropel","Leandro Agramont","Mateo Arnez"],
  "Real Suciedad":["Martino Moyano","Thiago Puebla","Lucio González","Juan Cruz Gutiérrez","Santiago Caldera","Calel Ronda","Mateo Juan","Filoma Valentino"],
  "Chispita Esperanza":["Tizi","Agus R","Lautaro G","Juanpi S","Dani Arce","Facu T","Martín Celis"],
  "Pinchila FC":["Tin","Bauti","Ciro","Ramy","Gero","Tomy"],
  "Chasquipom":["Joaquin Tirenti","Joaquin Gonzalez","Julian Peccinetti","Ignacio Lezcano","Parma Emilio Oggier Simón","Ignacio Cerda","Ruiz Gael","Bautista Caribe","Joaquin Villagra","Joaquin Rodriguez"],
  "Marisol FC":["Lautaro González","Emiliano Díaz","Lautaro Occhipinti","Fabrizio Ávila","Benjamín Muñoz","Valentino D'Ambrosio","Benjamín Acet","Maximo Ferreira"],
  "Viru FC":["Laureano Tomaselli","Tomás Gutierrez","Bautista Manno","Ticiano Moretti","Benjamin Olmedo","Thiago Kozusnik","Maximiliano Zorrilla","Facundo Bodar","David Mamani"]
};

// HORARIOS
const horarios = ["13:20","14:20","15:20"];
const canchas = ["Cancha 1","Cancha 2"];
const dias = ["Día 1","Día 2","Día 3"];

// PARTIDOS MANUALES PARA FASE REGULAR
const faseRegular = [
  {dia:1,cancha:1,hora:"13:20",A:"La Chispita ⚡️",B:"Viru FC"},
  {dia:1,cancha:2,hora:"13:20",A:"A la Lula",B:"La Favorita"},
  {dia:1,cancha:1,hora:"14:20",A:"Marcelu FC",B:"Real Suciedad"},
  {dia:1,cancha:2,hora:"14:20",A:"Chispita Esperanza",B:"Pinchila FC"},
  {dia:1,cancha:1,hora:"15:20",A:"Chasquipom",B:"Marisol FC"},
  {dia:2,cancha:1,hora:"13:20",A:"La Chispita ⚡️",B:"A la Lula"},
  {dia:2,cancha:2,hora:"13:20",A:"Viru FC",B:"Marcelu FC"},
  {dia:2,cancha:1,hora:"14:20",A:"La Favorita",B:"Chispita Esperanza"},
  {dia:2,cancha:2,hora:"14:20",A:"Real Suciedad",B:"Chasquipom"},
  {dia:2,cancha:1,hora:"15:20",A:"Pinchila FC",B:"Marisol FC"},
  {dia:3,cancha:1,hora:"13:20",A:"La Chispita ⚡️",B:"Marcelu FC"},
  {dia:3,cancha:2,hora:"13:20",A:"A la Lula",B:"Real Suciedad"},
  {dia:3,cancha:1,hora:"14:20",A:"Viru FC",B:"La Favorita"},
  {dia:3,cancha:2,hora:"14:20",A:"Chispita Esperanza",B:"Chasquipom"},
  {dia:3,cancha:1,hora:"15:20",A:"Pinchila FC",B:"Marisol FC"}
];

// SEMIFINALES Y FINAL
const faseFinal = [
  {fase:"Semifinal 1",cancha:1,hora:"15:50",A:"Ganador 1",B:"Ganador 2"},
  {fase:"Semifinal 2",cancha:2,hora:"15:50",A:"Ganador 3",B:"Ganador 4"},
  {fase:"Final",cancha:1,hora:"16:20",A:"Ganador SF1",B:"Ganador SF2"}
];

function crearPlanilla(teamA, teamB){
  const jugA = equipos[teamA] || ["Jugador TBD"];
  const jugB = equipos[teamB] || ["Jugador TBD"];
  const maxLen = Math.max(jugA.length,jugB.length);
  let html = `<table>
    <tr>
      <th>Jugador ${teamA}</th><th>Goles</th><th>🟨</th><th>🟥</th>
      <th>Jugador ${teamB}</th><th>Goles</th><th>🟨</th><th>🟥</th>
    </tr>`;
  for(let i=0;i<maxLen;i++){
    html+=`<tr>
      <td>${jugA[i]||""}</td><td><input></td><td><input></td><td><input></td>
      <td>${jugB[i]||""}</td><td><input></td><td><input></td><td><input></td>
    </tr>`;
  }
  html+=`</table><br>`;
  return html;
}

function mostrarFixture(){
  const fixtureDiv=document.getElementById("fixture");

  // Fase Regular
  dias.forEach(dia=>{
    const dayDiv=document.createElement("div");
    dayDiv.className="day";
    dayDiv.innerHTML=`<h2>${dia} – Fase Regular</h2>`;
    faseRegular.filter(p=>p.dia===parseInt(dia.slice(-1))).forEach(p=>{
      const matchDiv=document.createElement("div");
      matchDiv.className="match";
      matchDiv.innerHTML=`<div class="time">⏰ ${p.hora} - ${p.cancha}</div>
        <div class="teams">${p.A} 🆚 ${p.B}</div>
        ${crearPlanilla(p.A,p.B)}
      `;
      dayDiv.appendChild(matchDiv);
    });
    fixtureDiv.appendChild(dayDiv);
  });

  // Fase Final
  const finalDiv=document.createElement("div");
  finalDiv.className="fase";
  finalDiv.innerHTML=`<h2>⚔️ Fase Final</h2>`;
  faseFinal.forEach(p=>{
    const matchDiv=document.createElement("div");
    matchDiv.className="match";
    matchDiv.innerHTML=`<div class="time">⏰ ${p.hora} - Cancha ${p.cancha}</div>
      <div class="teams">${p.A} 🆚 ${p.B}</div>
      ${crearPlanilla(p.A,p.B)}
    `;
    finalDiv.appendChild(matchDiv);
  });
  fixtureDiv.appendChild(finalDiv);
}

mostrarFixture();
</script>
</body>
</html>
