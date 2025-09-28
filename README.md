<!DOCTYPE html>
<html>
<head>
  <title>Attendance Calculator</title>
  <style>
    body { font-family: Arial; background:#f5f5f5; text-align:center; }
    .container { margin:50px auto; padding:20px; background:#fff; width:400px; border-radius:10px; box-shadow:0 0 10px gray; }
    input { padding:10px; margin:10px; width:80%; }
    button { padding:10px 20px; background:#007bff; color:white; border:none; border-radius:5px; cursor:pointer; }
    h2 { color:#333; }
    #result { text-align:left; margin-top:20px; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Attendance Calculator</h2>
    <input type="number" id="totalLectures" placeholder="Total Lectures Conducted"><br>
    <input type="number" id="attendedLectures" placeholder="Lectures Attended"><br>
    <button onclick="calculateAttendance()">Calculate</button>
    <div id="result"></div>
  </div>

  <script>
    function calculateAttendance() {
      let total = parseInt(document.getElementById("totalLectures").value);
      let attended = parseInt(document.getElementById("attendedLectures").value);

      if (isNaN(total) || isNaN(attended) || total <= 0 || attended < 0 || attended > total) {
        document.getElementById("result").innerHTML = "<p style='color:red'>⚠️ Please enter valid numbers!</p>";
        return;
      }

      let percentage = (attended / total) * 100;
      let bunked = total - attended;
      let minRequired = Math.ceil(0.75 * total);
      let maxLeaves = total - minRequired;
      let remainingLeaves = maxLeaves - bunked;

      let msg = `
        <p><b>Total Lectures:</b> ${total}</p>
        <p><b>Lectures Attended:</b> ${attended}</p>
        <p><b>Lectures Bunked (Leaves Taken):</b> ${bunked}</p>
        <p><b>Your Attendance:</b> ${percentage.toFixed(2)}%</p>
        <p><b>Maximum Leaves Allowed:</b> ${maxLeaves}</p>
      `;

      if (remainingLeaves >= 0) {
        msg += `<p style='color:green'><b>✅ You can still take ${remainingLeaves} more leave(s).</b></p>`;
      } else {
        msg += `<p style='color:red'><b>⚠️ You have already exceeded the leave limit by ${Math.abs(remainingLeaves)}!</b></p>`;
      }

      document.getElementById("result").innerHTML = msg;
    }
  </script>
</body>
</html>
