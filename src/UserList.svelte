<script>
  let userList = getUser();

  async function getUser() {
    let response = await fetch("https://reqres.in/api/users");
    let userList = await response.json();
    if (response.ok) {
      return userList;
    } else {
      throw new Error(userList);
    }
  }
</script>

<style>
  .avatar {
    width: 4rem;
    height: 4rem;
    border-radius: 100px;
  }
  .list {
    list-style: none;
    padding: 0;
    margin-top: 2rem;
  }
  .listItem {
    height: 12vh;
    padding-left: 2rem;
    padding-top: 1rem;
    border-radius: 10px;
    box-shadow: 0px 4px 5px #aaa;
    margin-bottom: 1rem;
    transition: all 0.2s ease;
    background-color: #ffffff;
  }
  .listItem:hover {
    background-color: #357c93;
    color: white;
    font-weight: 600;
    box-shadow: 1px 1px 10px #aaa;
    transform: scale(1.1)
  }
  .listItem > img,
  .listItem > .itemText {
    float: left;
  }
  .listItem > .itemText {
    margin-left: 1rem;
    margin-bottom: 0;
    text-align: start;
  }
  @media (max-width: 425px) {
    .listItem {
      height: 14vh;
      padding-left: 1rem;
      padding-top: 1rem;
      box-shadow: 0px 4px 5px #aaa;
      border-radius: 10px;
      margin-bottom: 1rem;
    }
    .listItem > img {
      float: left;
    }
    .email {
      display: none;
    }
    .listItem > .itemText {
      margin-left: 2rem;
      margin-top: 1rem;
    }
    .avatar {
      margin-top: 1.3rem;
      width: 50px;
      height: 50px;
      border-radius: 100px;
    }
  }
</style>

{#await userList}
  <h4>Waiting...</h4>
{:then userList}
  <ul class="list">
    {#each userList.data as item}
      <li class="listItem">
        <img src={item.avatar} alt={item.avatar} class="avatar" />
        <div class="itemText">
          <p class="name">Name: {item.first_name} {item.last_name}</p>
          <p class="email">Email: {item.email}</p>
        </div>
      </li>
    {/each}
  </ul>
{/await}
