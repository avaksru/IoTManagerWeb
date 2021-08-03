<script>
	let url = "https://reqres.in/api/users?page=2";
	let configJSON;
	let res;
	let showprogress = [];
	let showerr = [];
	let showOK = [];

	//---------------- set /get data ------------------
	async function handleSubmit(url, id) {
		try {
			showprogress[id] = true;
			showerr[id] = false;
			showOK[id] = false;
			res = await fetch(url);

			if (res.ok) {
				console.log("OK", res.status);
				configJSON = await res.json();

				showprogress[id] = false;
				showerr[id] = false;
				showOK[id] = true;
			} else {
				console.log("error", res.status);
				showprogress[id] = false;
				showerr[id] = true;
				showOK[id] = false;
			}
		} catch (e) {
			console.log(e);
			showprogress[id] = false;
			showerr[id] = true;
			showOK[id] = false;
		}
	}
</script>

<button
	on:click={function () {
		handleSubmit(url, 1);
	}}
>
	123
</button>
<lable style="display : {showprogress[1] ? ' inline' : 'none'}">
	🙈 Загружаем данные</lable
>
<lable style="display : {showOK[1] ? ' inline' : 'none'}">
	✅ Данные успешно загружены</lable
>
<lable style="display : {showerr[1] ? ' inline' : 'none'}">
	💩 Не удалось получить данные</lable
>

<p>{configJSON ? JSON.stringify(configJSON) : ""}</p>
