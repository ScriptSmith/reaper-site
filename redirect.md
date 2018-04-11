# Values

<table>
<thead>
<tr>
<th>Argument</th>
<th>Value</th>
</tr>
</thead>
<tbody id='tablevalues'>
</tbody>
</table>


<script>
params = window.location.search.substr(1)
console.log(params)
param_arr = params.split("&")

for (var i=0; i<param_arr.length; i++) {
    couple = param_arr[i].split("=");
    tr = document.createElement('tr');
    arg = document.createElement('td');
    arg.innerHTML = couple[0];
    val = document.createElement('td');
    val.innerHTML = couple[1];
    tr.appendChild(arg)
    tr.appendChild(val)
    document.getElementById('tablevalues').appendChild(tr)
}
</script>