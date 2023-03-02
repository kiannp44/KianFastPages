<head>
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
</head>

## Tutors


<input id="search" placeholder="Search">
<button onclick="search()">Search</button>
<br>
<br>
<input id="tutorname" placeholder="Tutor Name">
<input id="age" placeholder="Age">
<input id="area" placeholder="Area">
<input id="contact" placeholder="Contact">
<button onclick="addTut()">Save</button>
<br>
<br>

<!-- Create table to display question posts -->

<table id="tutorTable" border="1" style="border-collapse: collapse;">
		<tr>
				<th>Id</th>
				<th>Tutor Name</th>
				<th>Age</th>
				<th>Area</th>
				<th>Contact</th>
		</tr>
</table>

<script>
  Tut();
  function Tut() {
  	const options = {
                method: 'GET', // *GET, POST, PUT, DELETE, etc.
                // mode: 'cors', // no-cors, *cors, same-origin
                cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
                // credentials: 'same-origin', // include, same-origin, omit
                headers: {
                'Content-Type': 'application/json'
                // 'Content-Type': 'application/x-www-form-urlencoded',
                },
            };
    const url = "https://hetvitrivedi.tk/api/tutor/";
    fetch(url, options)
      .then(res => res.json())
      .then(data => {
        console.log(data);
        console.log(typeof data);
        console.log(JSON.stringify(data));

		for (let i = 0; i < data.length; i++) {
			addTableRow(data[i].tutorname, data[i].age, data[i].area, data[i].contact);
		}
      });
  }

  function addTut() {
	const postOptions = {
                method: 'POST', // *GET, POST, PUT, DELETE, etc.
                // mode: 'cors', // no-cors, *cors, same-origin
                cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
                // credentials: 'same-origin', // include, same-origin, omit
                headers: {
                'Content-Type': 'application/json'
                // 'Content-Type': 'application/x-www-form-urlencoded',
                },
            };
	// var problemData = new URLSearchParams();
	// problemData.append(`problem`, document.getElementById("question").value);
	// problemData.append(`Unit`, document.getElementById("unit").value);
	// problemData.append(`Topic`, document.getElementById("topic").value);
	// problemData.append(`Tags`, document.getElementById("tags").value);
	var url = "https://hetvitrivedi.tk/api/tutor/add";
	url += "?name=" + document.getElementById("tutorname").value;
	url += "&Age=" + document.getElementById("age").value;
	url += "&Area=" + document.getElementById("area").value;
	url += "&Contact=" + document.getElementById("contact").value;
	// fetch the API
	fetch(url, postOptions)
	// response is a RESTful "promise" on any successful fetch
	.then(response => {
	// check for response errors
	if (response.status !== 200) {
		error("PUT API response failure: " + response.status)
		return;  // api failure
	}
	// valid response will have JSON data
	response.json().then(data => {
		console.log(data);
	})
	})
	// catch fetch errors (ie Nginx ACCESS to server blocked)
	.catch(err => {
	console.log(err + " ");
	});
  }
  function addTableRow(tutorname, age, area, contact) {
	let tableRow = document.createElement("tr");
	let idCell = document.createElement("td");
	tableRow.appendChild(idCell);
	let tutornameCell = document.createElement("td");
	tutornameCell.innerText = tutorname;
	tableRow.appendChild(tutornameCell);
	let ageCell = document.createElement("td");
	ageCell.innerText = age;
	tableRow.appendChild(ageCell);
	let areaCell = document.createElement("td");
	areaCell.innerText = area;
	tableRow.appendChild(areaCell);
	let contactCell = document.createElement("td");
	contactCell.innerText = contact;
	tableRow.appendChild(contactCell);

	document.getElementById("tutorTable").appendChild(tableRow);
  }

  function removeTableRows() {
	let numRows = document.getElementById("tutorTable").rows.length;
	for (let i = numRows-1; i > 0; i--) {
		document.getElementById("tutorTable").removeChild(document.getElementById("tutorTable").rows[i]);
	}
  }

</script>