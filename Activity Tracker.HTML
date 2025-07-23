<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Enhanced Employee Activity Logger</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    label, input, button { margin: 10px 5px; }
    table, th, td {
      border: 1px solid #ccc;
      border-collapse: collapse;
      padding: 8px;
      text-align: center;
    }
    table { width: 100%; margin-top: 20px; }
    th { background-color: #f4f4f4; }
    .summary-row td {
      font-weight: bold;
      background: #f9f9f9;
    }
    button:disabled {
      background: #ddd;
      color: #666;
      cursor: not-allowed;
    }
    .status-running { color: green; font-weight: bold; }
    .status-paused { color: orange; font-weight: bold; }
    .status-completed { color: gray; font-style: italic; }
    .status-notstarted { color: black; }
  </style>
</head>
<body>

<h2>Enhanced Employee Activity Logger</h2>

<div>
  <label for="usernameInput">Your Name:</label>
  <input type="text" id="usernameInput" placeholder="e.g. John Doe" />
  <button onclick="setUser()">Login</button>
</div>

<p>Today's Date: <span id="currentDate"></span></p>

<div>
  <label>Activity:</label>
  <input type="text" id="activityInput" placeholder="Describe activity" />
  <label>Project Code:</label>
  <input type="text" id="projectCodeInput" placeholder="Project code" />
  <button onclick="addNewActivity()">Add Activity</button>
</div>

<h3>Activity Log</h3>
<table>
  <thead>
    <tr>
      <th>User</th>
      <th>Date</th>
      <th>Activity</th>
      <th>Project Code</th>
      <th>Elapsed</th>
      <th>Status</th>
      <th>Comment</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody id="activityBody"></tbody>
  <tfoot>
    <tr class="summary-row">
      <td colspan="4">Total Hours</td>
      <td id="totalHours">0.00</td>
      <td colspan="3"></td>
    </tr>
  </tfoot>
</table>

<div style="margin-top: 30px;">
  <label>Start Date:</label>
  <input type="date" id="startDate" />
  <label>End Date:</label>
  <input type="date" id="endDate" />

  <label style="margin-left: 20px; display:none;" id="includeAllUsersLabel">
    <input type="checkbox" id="includeAllUsers" onchange="handleAllUsersCheck()" />
    Include All Users
  </label>

  <input type="password" id="adminPasscode" placeholder="Enter passcode" style="display:none; margin-left: 10px;" />

  <button onclick="downloadExcel()">Download Activities</button>
</div>

<script>
  let username = '';
  let isAdmin = false;
  let activities = [];
  let runningActivities = {};

  function setUser() {
    const input = document.getElementById('usernameInput');
    const enteredName = input.value.trim();
    if (!enteredName) {
      alert('Please enter your name.');
      return;
    }

    username = enteredName;
    isAdmin = (username.toLowerCase() === 'admin');
    alert(`Welcome, ${isAdmin ? 'Admin' : username}!`);

    if (isAdmin) {
      document.getElementById('includeAllUsersLabel').style.display = 'inline';
    } else {
      document.getElementById('includeAllUsersLabel').style.display = 'none';
      document.getElementById('includeAllUsers').checked = false;
      document.getElementById('adminPasscode').style.display = 'none';
    }

    renderActivityTable();
  }

  function updateDate() {
    document.getElementById('currentDate').textContent = new Date().toLocaleDateString();
  }

  function pad(n) {
    return n.toString().padStart(2, '0');
  }

  function formatDuration(seconds) {
    const h = Math.floor(seconds / 3600);
    const m = Math.floor((seconds % 3600) / 60);
    const s = seconds % 60;
    return `${pad(h)}:${pad(m)}:${pad(s)}`;
  }

  function handleAllUsersCheck() {
    document.getElementById('adminPasscode').style.display =
      document.getElementById('includeAllUsers').checked ? 'inline-block' : 'none';
  }

  function addNewActivity() {
    if (!username) return alert("Please log in first.");
    const activity = document.getElementById('activityInput').value.trim();
    const projectCode = document.getElementById('projectCodeInput').value.trim();
    if (!activity) return alert("Enter activity.");

    const newActivity = {
      id: Date.now(),
      user: username,
      dateAdded: new Date().toISOString(),
      activity,
      projectCode,
      elapsedSeconds: 0,
      status: 'Not Started',
      comment: []
    };

    activities.push(newActivity);
    saveActivitiesToStorage();
    document.getElementById('activityInput').value = '';
    document.getElementById('projectCodeInput').value = '';
    renderActivityTable();
  }

  function pauseActivity(id) {
    const activity = activities.find(a => a.id === id);
    if (!activity) return;
    const comment = prompt("Add a comment before pausing:", activity.comment?.join(" | ") || '');
    if (comment === null) return;

    const user = activity.user;
    const running = runningActivities[user];
    if (!running || running.id !== id || running.paused) return;

    clearInterval(running.timerInterval);
    running.elapsedBeforePause += Math.floor((Date.now() - running.startTime) / 1000);
    running.paused = true;

    activity.elapsedSeconds = running.elapsedBeforePause;
    activity.status = 'Paused';
    activity.comment.push(comment.trim());

    saveActivitiesToStorage();
    renderActivityTable();
  }

  function startActivity(id) {
    const activity = activities.find(a => a.id === id);
    const user = activity.user;

    if (runningActivities[user] && !runningActivities[user].paused) {
      return alert("You already have a running activity.");
    }

    runningActivities[user] = {
      id,
      startTime: Date.now(),
      elapsedBeforePause: activity.elapsedSeconds || 0,
      paused: false,
      timerInterval: setInterval(() => updateTimer(user), 1000)
    };

    activity.status = 'Running';
    saveActivitiesToStorage();
    renderActivityTable();
  }

  function resumeActivity(id) {
    const activity = activities.find(a => a.id === id);
    const user = activity.user;

    if (runningActivities[user] && !runningActivities[user].paused) {
      return alert("You already have a running activity.");
    }

    runningActivities[user] = {
      id,
      startTime: Date.now(),
      elapsedBeforePause: activity.elapsedSeconds || 0,
      paused: false,
      timerInterval: setInterval(() => updateTimer(user), 1000)
    };

    activity.status = 'Running';
    saveActivitiesToStorage();
    renderActivityTable();
  }

  function completeActivity(id) {
    const activity = activities.find(a => a.id === id);
    const comment = prompt("Enter a comment before completing:", '');
    if (!comment) return alert("Completion comment required.");

    const user = activity.user;
    const running = runningActivities[user];

    if (running && running.id === id) {
      clearInterval(running.timerInterval);
      if (!running.paused) {
        running.elapsedBeforePause += Math.floor((Date.now() - running.startTime) / 1000);
      }
      delete runningActivities[user];
    }

    activity.elapsedSeconds = running?.elapsedBeforePause || activity.elapsedSeconds;
    activity.status = 'Completed';
    activity.comment.push(comment.trim());

    saveActivitiesToStorage();
    renderActivityTable();
  }

  function deleteActivity(id) {
    const pass = prompt("Enter admin passcode to delete:");
    if (pass !== '00001234' || !isAdmin) return alert("Wrong passcode or unauthorized.");
    activities = activities.filter(a => a.id !== id);
    saveActivitiesToStorage();
    renderActivityTable();
  }

  function updateTimer(user) {
    const running = runningActivities[user];
    if (!running || running.paused) return;
    const now = Date.now();
    const elapsed = running.elapsedBeforePause + Math.floor((now - running.startTime) / 1000);
    const activity = activities.find(a => a.id === running.id);
    if (activity) activity.elapsedSeconds = elapsed;
    saveActivitiesToStorage();
    renderActivityTable();
  }

  function renderActivityTable() {
    const tbody = document.getElementById('activityBody');
    tbody.innerHTML = '';
    let totalSeconds = 0;

    const visibleActivities = activities.filter(act => isAdmin || act.user === username);

    visibleActivities.forEach(act => {
      const tr = document.createElement('tr');
      tr.innerHTML = `
        <td>${act.user}</td>
        <td>${new Date(act.dateAdded).toLocaleDateString()}</td>
        <td>${act.activity}</td>
        <td>${act.projectCode}</td>
        <td>${formatDuration(act.elapsedSeconds || 0)}</td>
        <td class="status-${act.status.toLowerCase().replace(' ', '')}">
          ${act.status === 'Running' ? '🟢 Running' :
            act.status === 'Paused' ? '⏸️ Paused' :
            act.status === 'Completed' ? '✔️ Completed' : 'Not Started'}
        </td>
        <td>${Array.isArray(act.comment) ? act.comment.join(" | ") : act.comment || ''}</td>
        <td></td>
      `;

      const actions = tr.lastElementChild;

      const btnStart = document.createElement('button');
      btnStart.textContent = 'Start';
      btnStart.disabled = act.status === 'Completed';
      btnStart.onclick = () => startActivity(act.id);
      actions.appendChild(btnStart);

      if (act.status === 'Running') {
        const btnPause = document.createElement('button');
        btnPause.textContent = 'Pause';
        btnPause.onclick = () => pauseActivity(act.id);
        actions.appendChild(btnPause);
      }

      if (act.status === 'Paused') {
        const btnResume = document.createElement('button');
        btnResume.textContent = 'Resume';
        btnResume.onclick = () => resumeActivity(act.id);
        actions.appendChild(btnResume);
      }

      const btnComplete = document.createElement('button');
      btnComplete.textContent = 'Complete';
      btnComplete.disabled = act.status === 'Completed';
      btnComplete.onclick = () => completeActivity(act.id);
      actions.appendChild(btnComplete);

      const btnDelete = document.createElement('button');
      btnDelete.textContent = 'Delete';
      btnDelete.onclick = () => deleteActivity(act.id);
      actions.appendChild(btnDelete);

      tbody.appendChild(tr);
      totalSeconds += act.elapsedSeconds || 0;
    });

    document.getElementById('totalHours').textContent = (totalSeconds / 3600).toFixed(2);
  }

  function saveActivitiesToStorage() {
    localStorage.setItem('activityLogs', JSON.stringify(activities));
  }

  function loadActivitiesFromStorage() {
    const data = localStorage.getItem('activityLogs');
    if (data) {
      activities = JSON.parse(data);
    }
  }

 function downloadExcel() {
    const includeAll = document.getElementById('includeAllUsers').checked;
    const pass = document.getElementById('adminPasscode').value;

    if (includeAll && (!isAdmin || pass !== '00001234')) {
      alert('Invalid admin passcode.');
      return;
    }

    const start = new Date(document.getElementById('startDate').value);
    const end = new Date(document.getElementById('endDate').value);
    if (!isNaN(end)) end.setHours(23, 59, 59, 999);

    const filtered = activities.filter(a => {
      const date = new Date(a.dateAdded);
      return (!isNaN(start) ? date >= start : true) &&
             (!isNaN(end) ? date <= end : true) &&
             (includeAll && isAdmin ? true : a.user === username);
    });

    if (filtered.length === 0) {
      alert('No activities found.');
      return;
    }

    const ws_data = [['User', 'Date', 'Activity', 'Project Code', 'Hours', 'Status', 'Comment']];
    filtered.forEach(act => {
      const comments = Array.isArray(act.comment) ? act.comment.join(" | ") : act.comment || '';
      const fullComment = `Activity: ${act.activity}` + (comments ? ` | ${comments}` : '');

      ws_data.push([
        act.user,
        new Date(act.dateAdded).toLocaleDateString(),
        act.activity,
        act.projectCode,
        ((act.elapsedSeconds || 0) / 3600).toFixed(2),
        act.status,
        fullComment
      ]);
    });

    const total = filtered.reduce((s, a) => s + (a.elapsedSeconds || 0), 0);
    ws_data.push(['', '', '', 'Total Hours', (total / 3600).toFixed(2)]);

    const wb = XLSX.utils.book_new();
    const ws = XLSX.utils.aoa_to_sheet(ws_data);
    XLSX.utils.book_append_sheet(wb, ws, "Activities");
    XLSX.writeFile(wb, `activity_log_${new Date().toISOString().slice(0,10)}.xlsx`);
  }

  // Initialize
  updateDate();
  loadActivitiesFromStorage();
  renderActivityTable();
  setInterval(updateDate, 1000 * 60 * 60);
</script>
</body>
</html>
