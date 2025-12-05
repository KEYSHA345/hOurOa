<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Houro</title>

<link href="https://fonts.googleapis.com/css2?family=Open+Sans&family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: "Poppins", sans-serif;
    background: linear-gradient(135deg, #7b68ee, #6a5acd);
    background-attachment: fixed;
    background-size: cover;
    color: white;
    overflow-x: hidden;
  }

  /* NAVBAR */
  .navbar {
    height: 60px; 
    background: rgba(255,255,255,0.8);
    backdrop-filter: blur(8px);
    display: flex; 
    justify-content: center; 
    align-items: center; 
    gap: 20px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    position: sticky;
    top: 0;
    z-index: 1000;
  }
  .nav-links { display: flex; gap: 15px; }
  .nav-links a {
    text-decoration: none; 
    color: black; 
    font-size: 18px; 
    font-weight: bold; 
    border: 2px solid black; 
    padding: 5px 12px; 
    border-radius: 6px;
    cursor: pointer; 
    transition: all 0.3s ease;
  }
  .nav-links a:hover, .nav-links a.active-link { 
    color: #6a0dad; 
    border-color: #6a0dad; 
    box-shadow: 0 0 10px rgba(106,13,173,0.4);
  }

  /* SECTIONS */
  section {
    width: 90%;
    max-width: 1000px;
    margin: 0 auto;
    text-align: center;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  section.active {
    opacity: 1;
    transform: translateY(0);
  }

  /* HOMEPAGE */
  #home { 
    display: flex; 
    flex-direction: column; 
    justify-content: center; 
    align-items: center; 
    height: calc(100vh - 60px); 
    text-align: center;
  }
  #home .homepage-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  #home .logo img {
    width: clamp(200px, 50vw, 400px);
    height: auto;
    display: block;
    margin: 10px auto 5px;
    transition: transform 0.4s ease, filter 0.5s ease;
    filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.4));
  }
  #home .logo img:hover {
    transform: scale(1.05);
    filter: drop-shadow(0 0 15px rgba(255, 255, 255, 0.7));
  }
  .catchphrase {
    font-size: 1.8rem;
    font-weight: 600;
    margin-top: 16px;
    color: #ffffff;
    text-shadow: 0 0 6px rgba(0, 0, 0, 0.3);
  }

  /* TASKS */
  #tasks {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    min-height: calc(100vh - 60px);
    padding-top: 10px;
  }
  #tasks .container {
    margin: 40px auto;
    max-width: 900px;
    text-align: center;
  }
  #tasks h1 { text-align: center; margin-bottom: 25px; color: #2c3e50; }
  #tasks form { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; margin-bottom: 30px; }
  #tasks input[type="text"], #tasks input[type="date"] { 
    padding: 12px; font-size: 16px; width: 220px; 
    border: 1px solid #ccc; border-radius: 6px;
  }
  #tasks button { 
    padding: 12px 24px; font-size: 16px; 
    background-color: #2c3e50; color: white; 
    border: none; border-radius: 8px; 
    cursor: pointer; transition: 0.3s;
  }
  #tasks button:hover { background-color: #1a252f; }

  /* Show All Tasks button */
  #showAllTasks {
    margin-top: 20px;  
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 8px;
    border: none;
    background-color: #2c3e50;
    color: white;
    cursor: pointer;
  }
  #showAllTasks:hover { background-color: #1a252f; }

  #tasks ul { list-style-type: none; padding: 0; display: grid; grid-template-columns: repeat(auto-fill,minmax(250px,1fr)); gap: 15px; }
  #tasks li.task { 
    padding: 12px 15px; margin-bottom: 10px; 
    border-radius: 10px; font-size: 17px; 
    display: flex; flex-direction: column;
    justify-content: space-between; 
    color: white; 
    min-height: 80px;
  }
  .task-btns { margin-top: 8px; display: flex; justify-content: flex-end; }
  .task-btns button { margin-left: 8px; border: none; border-radius: 4px; cursor: pointer; padding: 5px 8px; font-weight: bold; transition: 0.2s; }
  .edit-btn { background-color: #3498db; color: white; }
  .save-btn { background-color: #27ae60; color: white; }
  .cancel-btn { background-color: #e67e22; color: white; }
  .delete-btn { background-color: white; color: #2c3e50; }
  .overdue { background-color: #e74c3c; }
  .due-soon { background-color: #f1c40f; color: #333; }
  .due-later { background-color: #2ecc71; }

  /* CALENDAR */
  #calendar-section {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: calc(100vh - 60px);
  }
  #calendar-section .container {
    width: 85%;
    max-width: 900px;
    background-color: rgba(255, 255, 255, 0.7);
    border-radius: 15px;
    padding: 25px 35px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    position: relative;
    overflow: hidden;

    /* background fit */
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
  }
  .calendar-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
  .calendar-header button { background: #2c3e50; color: white; border: none; padding: 8px 12px; border-radius: 5px; cursor: pointer; font-weight: 600; }
  .calendar-header button:hover { background: #1a252f; }
  .calendar-header h2 { font-family: 'Poppins', sans-serif; font-size: 22px; }
  .calendar { display: grid; grid-template-columns: repeat(7, 1fr); gap: 5px; }
  .calendar-header h2, .day-number, .day-header { color: #000 !important; }
  .day { min-height: 80px; border: 1px solid #ccc; border-radius: 5px; padding: 5px; background: #fafafa; overflow-y: auto; cursor: pointer; }
  .day-number { font-weight: bold; margin-bottom: 5px; }
  .task-red { background-color: #ffb3b3; color: #900; padding: 2px 4px; border-radius: 4px; margin-top: 2px; display: block; font-size: 0.8em; }
  .task-yellow { background-color: #fff1b8; color: #a67c00; padding: 2px 4px; border-radius: 4px; margin-top: 2px; display: block; font-size: 0.8em; }
  .task-green { background-color: #d4edda; color: #155724; padding: 2px 4px; border-radius: 4px; margin-top: 2px; display: block; font-size: 0.8em; }
  .current-day { background-color: #d3d3d3; border-radius: 8px; color: #000; font-weight: bold; }
  #gotoDate { margin: 10px 5px 20px; padding: 8px; }
  #gotoDateBtn { padding: 8px 12px; }
</style>
</head>
<body>

<!-- NAVBAR -->
<div class="navbar">
  <div class="nav-links">
    <a href="#" onclick="showSection('home'); setActiveLink(this); return false;">Homepage</a>
    <a href="#" onclick="showSection('tasks'); setActiveLink(this); return false;">Tasks</a>
    <a href="#" onclick="showSection('calendar-section'); setActiveLink(this); return false;">Calendar</a>
  </div>
</div>

<!-- HOMEPAGE -->
<section id="home" class="active">
  <div class="homepage-content">
    <h3 class="catchphrase"><b>Every Hour Planned, Life Lived Better.</b></h3>
    <div class="logo">
      <img src="Houro_logo.png" alt="Houro Logo" />
    </div>
    <p>HOURO</p>
  </div>
</section>

<!-- TASKS -->
<section id="tasks">
  <div class="container">
    <h1>Task Manager</h1>
    <form id="taskForm">
      <input type="text" id="taskName" placeholder="Task name" required />
      <input type="date" id="taskDate" required />
      <button type="submit">Add Task</button>
    </form>
    <ul id="taskList"></ul>
    <button id="showAllTasks">Show All Tasks</button>
  </div>
</section>

<!-- CALENDAR -->
<section id="calendar-section">
  <div class="container">
    <input type="file" id="bgUpload" accept="image/*" />
    <div>
      <input type="date" id="gotoDate" />
      <button id="gotoDateBtn">Go To Date</button>
    </div>
    <div class="calendar-header">
      <button id="prevMonth">← Prev</button>
      <h2 id="monthLabel"></h2>
      <button id="nextMonth">Next →</button>
    </div>
    <div class="calendar" id="calendar"></div>
  </div>
</section>

<script>
  // NAVIGATION
  function setActiveLink(link) {
    document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active-link'));
    link.classList.add('active-link');
  }

  function showSection(sectionId) {
    document.querySelectorAll("section").forEach(sec => {
      sec.classList.remove("active");
      sec.style.display = "none";
    });

    const activeSection = document.getElementById(sectionId);

    if(sectionId === 'home') {
      activeSection.style.display = 'flex';
      activeSection.style.flexDirection = 'column';
      activeSection.style.justifyContent = 'center';
      activeSection.style.alignItems = 'center';
      activeSection.style.textAlign = 'center';
      activeSection.style.height = 'calc(100vh - 60px)';
    } else {
      activeSection.style.display = 'block';
    }

    setTimeout(() => activeSection.classList.add("active"), 10);
  }

  // TASK STORAGE
  function loadTasks(){ return JSON.parse(localStorage.getItem('tasks')||'[]'); }
  function saveTasks(tasks){ localStorage.setItem('tasks', JSON.stringify(tasks)); }

  function renderTaskList(filterDate=null){
    const tasks = loadTasks();
    const taskList = document.getElementById('taskList');
    taskList.innerHTML='';
    const today = new Date(); today.setHours(0,0,0,0);

    tasks.forEach((task,index)=>{
      const taskDate = new Date(task.date); taskDate.setHours(0,0,0,0);
      if(filterDate && taskDate.getTime()!==filterDate.getTime()) return;

      const li=document.createElement('li'); li.classList.add('task');
      const diff=(taskDate-today)/(1000*60*60*24);
      li.classList.add(diff<0?'overdue':diff<=3?'due-soon':'due-later');

      const span=document.createElement('span');
      span.textContent=`${task.name} (Due: ${taskDate.toDateString()})`;

      const btnGroup=document.createElement('div'); btnGroup.classList.add('task-btns');
      const editBtn=document.createElement('button'); editBtn.textContent='✏️'; editBtn.classList.add('edit-btn');
      editBtn.addEventListener('click',()=>enterEditMode(index,li,task));
      const delBtn=document.createElement('button'); delBtn.textContent='✔'; delBtn.classList.add('delete-btn');
      delBtn.addEventListener('click',()=>{
        tasks.splice(index,1); saveTasks(tasks); renderTaskList(); renderCalendar();
      });

      btnGroup.append(editBtn, delBtn);
      li.append(span, btnGroup);
      taskList.appendChild(li);
    });
  }

  function enterEditMode(index,li,task){
    li.innerHTML='';
    const nameInput=document.createElement('input'); nameInput.type='text'; nameInput.value=task.name;
    const dateInput=document.createElement('input'); dateInput.type='date'; dateInput.value=task.date;
    const saveBtn=document.createElement('button'); saveBtn.textContent='💾'; saveBtn.classList.add('save-btn');
    saveBtn.addEventListener('click',()=>{
      const tasks=loadTasks(); tasks[index]={name:nameInput.value.trim(),date:dateInput.value}; saveTasks(tasks);
      renderTaskList(); renderCalendar();
    });
    const cancelBtn=document.createElement('button'); cancelBtn.textContent='❌'; cancelBtn.classList.add('cancel-btn');
    cancelBtn.addEventListener('click',()=>renderTaskList());
    li.append(nameInput,dateInput,saveBtn,cancelBtn);
  }

  document.getElementById('taskForm').addEventListener('submit', e=>{
    e.preventDefault();
    const name=document.getElementById('taskName').value.trim();
    const date=document.getElementById('taskDate').value;
    if(!name||!date) return;
    const tasks=loadTasks(); tasks.push({name,date}); saveTasks(tasks);
    document.getElementById('taskForm').reset();
    renderTaskList(); renderCalendar();
  });

  document.getElementById('showAllTasks').addEventListener('click',()=>renderTaskList());

  // CALENDAR
  let currentDate = new Date();
  const calendarEl=document.getElementById('calendar');
  const monthLabel=document.getElementById('monthLabel');

  function renderCalendar(){
    calendarEl.innerHTML='';
    const year=currentDate.getFullYear();
    const month=currentDate.getMonth();
    monthLabel.textContent=currentDate.toLocaleString('default',{month:'long',year:'numeric'});
    const firstDay=new Date(year,month,1).getDay();
    const lastDate=new Date(year,month+1,0).getDate();
    const tasks=loadTasks().map(t=>({name:t.name,date:new Date(t.date)}));

    ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'].forEach(d=>{
      const dh=document.createElement('div'); dh.textContent=d; dh.classList.add('day-header'); calendarEl.appendChild(dh);
    });
    for(let i=0;i<firstDay;i++){ const empty=document.createElement('div'); empty.classList.add('day'); calendarEl.appendChild(empty); }

    for(let d=1;d<=lastDate;d++){
      const dayEl=document.createElement('div'); dayEl.classList.add('day');
      const dayNumber=document.createElement('div'); dayNumber.classList.add('day-number'); dayNumber.textContent=d;
      const thisDate=new Date(year,month,d); thisDate.setHours(0,0,0,0);
      const today=new Date(); today.setHours(0,0,0,0);
      if(thisDate.getTime()===today.getTime()) dayEl.classList.add('current-day');

      tasks.forEach(t=>{
        if(t.date.getFullYear()===year && t.date.getMonth()===month && t.date.getDate()===d){
          const diff=(t.date-today)/(1000*60*60*24);
          const span=document.createElement('span');
          span.textContent=t.name;
          span.classList.add(diff<0?'task-red':diff<=3?'task-yellow':'task-green');
          dayEl.appendChild(span);
        }
      });

      dayEl.addEventListener('click',()=>{ 
        highlightTasksForDate(thisDate);
      });

      dayEl.prepend(dayNumber);
      calendarEl.appendChild(dayEl);
    }
  }

  document.getElementById('prevMonth').addEventListener('click',()=>{ currentDate.setMonth(currentDate.getMonth()-1); renderCalendar(); });
  document.getElementById('nextMonth').addEventListener('click',()=>{ currentDate.setMonth(currentDate.getMonth()+1); renderCalendar(); });

  function highlightTasksForDate(date){
    showSection('tasks');
    renderTaskList(date);
  }

  document.getElementById('gotoDateBtn').addEventListener('click',()=>{
    const val=document.getElementById('gotoDate').value;
    if(!val) return;
    const parts=val.split('-');
    currentDate=new Date(parts[0],parts[1]-1,1);
    renderCalendar();
  });

  // BACKGROUND IMAGE
  const bgInput=document.getElementById('bgUpload');
  const calendarContainer=document.querySelector('#calendar-section .container');

  bgInput.addEventListener('change',e=>{
    const file=e.target.files[0];
    if(!file) return;
    const reader=new FileReader();
    reader.onload=e=>{
      calendarContainer.style.backgroundImage=`url(${e.target.result})`;
      calendarContainer.style.backgroundSize='contain';
      calendarContainer.style.backgroundPosition='center';
      calendarContainer.style.backgroundRepeat='no-repeat';
      localStorage.setItem('calendarBg',e.target.result);
    }
    reader.readAsDataURL(file);
  });

  window.addEventListener('load',()=>{
    const bg=localStorage.getItem('calendarBg');
    if(bg){
      calendarContainer.style.backgroundImage=`url(${bg})`;
      calendarContainer.style.backgroundSize='contain';
      calendarContainer.style.backgroundPosition='center';
      calendarContainer.style.backgroundRepeat='no-repeat';
    }
    renderTaskList();
    renderCalendar();
  });
</script>

</body>
</html>
