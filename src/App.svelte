<script>
  import UserList from "./UserList.svelte";
</script>

<style>
  h1 {
    color: #357c93;
    text-transform: uppercase;
    font-weight: 300;
    font-size: 3rem
  }
  .row {
    text-align: center;
  }
  .list {
    margin: auto;
    width: 30vw
  }
  @media (max-width: 425px) {
    .list {
      width: 90vw;
    }
  }
  @media (min-width: 426px) and (max-width: 768px) {
    .list {
      width: 50vw;
    }
  }
  @media (min-width: 769px) and (max-width: 1024px) {
    .list {
      width: 40vw;
    }
  }
</style>

<div class="container">
  <div class="row">
    <h1>user list</h1>
  </div>
  <div class="row list">
    <UserList />
  </div>
</div>
