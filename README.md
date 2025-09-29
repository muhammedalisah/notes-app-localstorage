# notes-app-localstorage
notes-app-localstorage
# Notes App
Tarayıcı LocalStorage kullanan basit not uygulaması.
<!doctype html>
<html>
<head><meta charset="utf-8"><title>Notes</title></head>
<body>
<h1>Notes</h1>
<input id="noteInput" placeholder="Yeni not">
<button onclick="addNote()">Add</button>
<ul id="notes"></ul>
<script>
function load(){
  const notes = JSON.parse(localStorage.getItem("notes")||"[]");
  const ul = document.getElementById("notes");
  ul.innerHTML = "";
  notes.forEach((n,i)=> {
    const li = document.createElement("li");
    li.textContent = n + " ";
    const btn = document.createElement("button");
    btn.textContent = "Sil";
    btn.onclick = ()=>{ notes.splice(i,1); localStorage.setItem("notes", JSON.stringify(notes)); load();};
    li.appendChild(btn);
    ul.appendChild(li);
  });
}
function addNote(){
  const input = document.getElementById("noteInput");
  const notes = JSON.parse(localStorage.getItem("notes")||"[]");
  if(input.value.trim() === "") return;
  notes.push(input.value.trim());
  localStorage.setItem("notes", JSON.stringify(notes));
  input.value = "";
  load();
}
load();
</script>
</body>
</html>
