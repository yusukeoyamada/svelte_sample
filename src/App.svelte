<script>
	import ToDoInputForm from "./ToDoInputForm.svelte"
  import ToDoList from "./ToDoList.svelte"
  let nameEntered = false

  let lastName = ""
  let firstName = ""

  // リアクティブ宣言「$:」を使用して
  // 変数と変数を同期させて維持させる
  $: fullName = lastName + " " + firstName

  function handleSubmit() {
    if (lastName && firstName) {
      nameEntered = true
    }
  }
</script>

<main>
{#if nameEntered}
  <h1>タスクリストアプリケーションへようこそ、{fullName}さん!</h1>
	<ToDoInputForm userName={fullName}/>
  <ToDoList />
{:else}
  <h1>タスクリストアプリケーションへようこそ!</h1>
  <h3>名前を入力してください。</h3>

  <!-- フォームは、デフォルトの動作として、form要素に送信先が指定されていない場合、
  現在のURLに対してフォームの内容を送信します。
  現在のURLに対してフォームの送信が行われると、ページが自動的にリロードされてしまいます。
  この動作を防ぐために、「event.preventDefault()」を走らせます。 -->
  <form on:submit|preventDefault={handleSubmit}>

    <!-- 「bind:value」により、input要素に入力される値は、{lastName}や、{firstName}変数に紐付けられます。
    この紐付けにより、データを双方向で同期させることができます。 -->
      <!-- ユーザーが入力要素の値を変更すると、それに応じて値が更新される -->
    <div>
      <input bind:value={lastName} type="text" placeholder="姓" required>
    </div>
    <div>
      <input bind:value={firstName} type="text" placeholder="名" required>
    </div>
    <button type="submit">タスク管理を始める</button>
  </form>
{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 450px;
		margin: 0 auto;
	}
</style>
