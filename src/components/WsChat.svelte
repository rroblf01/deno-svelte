<script lang="ts">
  import ListMessages from "./ListMessages.svelte";
  import ListUsers from "./ListUsers.svelte";

  export let name = "Stranger";
  export let isLogged = true;

  let myComment = "";

  let commentList: string[] = [];
  let userList: string[] = [];

  function newComment() {
    ws.send(JSON.stringify({ type: "newComment", message: myComment }));
    myComment = "";
  }

  function closeConnection() {
    ws.close();
    isLogged = false;
  }
  const ws = new WebSocket("wss://ricardo-chat.deno.dev/websocket");
  ws.onopen = () => {
    ws.send(JSON.stringify({ type: "newUser", name }));
  };

  ws.onmessage = (m) => {
    const response = JSON.parse(m.data);
    if (response.type === "newUser") {
      userList = response.names;
    } else if (response.type === "newComment") {
      commentList = response.comments;
    }
  };
</script>

<main class="flex-container">
  <div class="flex-item">
    <h3>Usuarios conectados</h3>
    <ListUsers componentList={userList} />
    <button on:click={closeConnection}>Logout</button>
  </div>

  <div class="flex-item">
    <p>¡Hola {name}!</p>
    <ListMessages componentList={commentList} />
    <textarea
      class="new-message"
      bind:value={myComment}
      on:keydown={(event) => event.key === "Enter" && newComment()}
      placeholder="Enter your comment"
    />
  </div>
</main>

<style>
  .new-message {
    font-size: 1.4em;
    width: 60vh;
    margin: 10px;
    resize: none;
  }

  .flex-container {
    display: flex;
    flex-direction: row;
    font-size: 25px;
    text-align: center;
    justify-content: flex-end;
  }

  .flex-item {
    padding: 10px;
    flex: 50%;
  }

  main {
    max-width: 36em;
    margin: 0 auto;
    text-align: center;
  }

  @media (max-width: 800px) {
    .flex-item {
      flex: 100%;
    }
    .flex-container {
      flex-direction: column;
    }
  }
</style>
