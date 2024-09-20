<script lang="ts">
  import { onMount } from "svelte";

  type Root = {
    page: number;
    per_page: number;
    total: number;
    total_pages: number;
    data: Daum[];
    support: Support;
  };

  type Daum = {
    id: number;
    email: string;
    first_name: string;
    last_name: string;
    avatar: string;
  };

  type Support = {
    url: string;
    text: string;
  };

  let users:any
  let page = 1;

  onMount(async () => {
    console.log("page", page)
    users = await getUsers(String(page));
  });

  async function getUsers(page: string) {
    let response = await fetch(
      `https://reqres.in/api/users${page ? "?page=" + page : ""}`,
    );
    let userList = await response.json();
    if (response.ok) {
      return userList;
    } else {
      throw new Error(userList);
    }
  }

  async function clickPageButton (direction: string) {
    if (direction === "prev") {
      page -= 1
    } else {
      page += 1
    }
    users = await getUsers(String(page))
  }
</script>

{#if users}
<button class="btn" disabled={page <= 1} on:click={() => clickPageButton("prev")}>BACK</button>
<button class="btn" disabled={page == users.total_pages} on:click={() => clickPageButton("next")}>NEXT</button>
<ul class="list">
  {#if Object.hasOwn(users, "data")}
  {#each users.data as item}
    <li class="listItem">
      <img src={item.avatar} alt={item.avatar} class="avatar" />
      <div class="itemText">
        <p class="name">Name: {item.first_name} {item.last_name}</p>
        <p class="email">Email: {item.email}</p>
      </div>
    </li>
  {/each}
  {/if}
</ul>
{/if}

<!-- {#await users}
  <h4>Waiting...</h4>
{:then users}
  <ul class="list">
      {#if Object.hasOwn(users, "data")}
      {#each users.data as item}
        <li class="listItem">
          <img src={item.avatar} alt={item.avatar} class="avatar" />
          <div class="itemText">
            <p class="name">Name: {item.first_name} {item.last_name}</p>
            <p class="email">Email: {item.email}</p>
          </div>
        </li>
      {/each}
      {/if}
    </ul>
{/await} -->

<style>
  .btn {
    border-radius: 5px;
    border: 0;
    color: #FFF;
    font-size: large;
    font-weight: 700;
    background-color: #357c93;
  }
  .btn:hover {
    border-radius: 5px;
    border: 0;
    color: #FFF;
    font-weight: 700;
    background-color: #45aed1;
    cursor: pointer;
  }
  .btn:disabled {
    border-radius: 5px;
    border: 0;
    color: #FFF;
    font-weight: 700;
    background-color: #383c3d;
    cursor: not-allowed;
  }
  .avatar {
    width: 4rem;
    height: 4rem;
    border-radius: 100px;
  }
  .list {
    list-style: none;
    padding: 0;
    padding-bottom: 1rem;
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
    transform: scale(1.1);
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
