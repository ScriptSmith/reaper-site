# Excel date & time formulas

In order to interpret the columns that contain temporal information from each of the platforms that Reaper supports, you need to apply specific forumulas.

Rather than figuring them out yourself, you can get them from this page.

## 1. Choose your platform

<select id='platform' onchange='calcFormula()'>
  <option value="DATE(MID(%%,1,4),MID(%%,6,2),MID(%%,9,2))|TIME(MID(%%,12,2),MID(%%,15,2),MID(%%,18,2))">Facebook</option>
  <option value="DATE(MID(%%,27,4),MONTH(DATEVALUE(MID(%%,5,3)&1)),MID(%%,9,2))|TIME(MID(%%,12,2),MID(%%,15,2),MID(%%,18,2))">Twitter</option>
  <option value="(((%%/60)/60)/24)+DATE(1970,1,1)|(%%/86400)+25569">Reddit</option>
  <option value="DATE(MID(%%,1,4),MID(%%,6,2),MID(%%,9,2))|TIME(MID(%%,12,2),MID(%%,15,2),MID(%%,18,2))">YouTube</option>
  <option value="DATE(MID(%%,1,4),MID(%%,6,2),MID(%%,9,2))|TIME(MID(%%,12,2),MID(%%,15,2),MID(%%,18,2))">Tumblr</option>
</select>

## 2. Type the name of your cell
Cell name: <input type="text" placeholder='C2' id='cell' onkeyup='calcFormula()'>

## 3. Copy the formula


Date: <input type='text' id='date' value='Hi'> <button onclick='copy(date)'>Copy to clipboard</button><br>
Time: <input type='text' id='time' value='Hi'> <button onclick='copy(time)'>Copy to clipboard</button><br>
DateTime: <input type='text' id='datetime' value='Hi'> <button onclick='copy(datetime)'>Copy to clipboard</button>

<script>
var platform = document.getElementById('platform');
var cell = document.getElementById('cell');
var date = document.getElementById('date');
var time = document.getElementById('time');
var datetime = document.getElementById('datetime');

function copy(element) {
    element.select();
    document.execCommand("Copy");
}

function calcFormula() {
    var valSplit = platform.options[platform.selectedIndex].value.split("|")
    date.value = '=' + valSplit[0].replace(/%%/g, cell.value);
    time.value = '=' + valSplit[1].replace(/%%/g, cell.value);
    datetime.value = '=' + valSplit[0].replace(/%%/g, cell.value) + " + " + valSplit[1].replace(/%%/g, cell.value);
}
calcFormula();
</script>
