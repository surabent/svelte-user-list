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
<div class="page-btn">
  <button class="btn" disabled={page <= 1} on:click={() => clickPageButton("prev")}>BACK</button>
</div>
<div>
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
</div>
<div class="page-btn">
  <button class="btn" disabled={page == users.total_pages} on:click={() => clickPageButton("next")}>NEXT</button>
</div>
<div class="mobile-page-btn">
  <button class="btn" disabled={page <= 1} on:click={() => clickPageButton("prev")}>BACK</button>
  <button class="btn" disabled={page == users.total_pages} on:click={() => clickPageButton("next")}>NEXT</button>
</div>
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
    display: flex;
    flex-direction: column;
    padding: 0;
    gap: 0.5rem;
  }
  .listItem {
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0px 4px 5px #aaa;
    transition: all 0.2s ease;
    background-color: #ffffff;
    min-width: 20rem;
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
    text-align: start;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
  .listItem > .itemText p {
    margin: 0;
  }
  .page-btn {
    align-self: center;
    justify-self: center;
  }
  @media (max-width: 768px) {
    .listItem {
      padding: 1rem;
      box-shadow: 0px 4px 5px #aaa;
      border-radius: 10px;
      min-width: 20rem;
    }
    .listItem > img {
      float: left;
    }
    .avatar {
      width: 50px;
      height: 50px;
      border-radius: 100px;
    }
    .page-btn {
      display: none;
    }
    .mobile-page-btn {
      display: flex;
      justify-content: center;
      gap: 1rem;
    }
  }
  @media (min-width: 768px) {
    .mobile-page-btn {
      display: none;
    }
  }
</style>
