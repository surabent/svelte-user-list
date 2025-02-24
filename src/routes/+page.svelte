  <script>
    import Userlist from "$lib/Userlist.svelte";
  </script>
  <style>
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 1rem;
      gap: 1rem;
    }
    .header {
      text-transform: uppercase;
      font-weight: 600;
      font-size: 2rem;
      margin-top: 0;
      margin-bottom: 5px;
    }
    .user-list {
      display: flex;
      gap: 4rem;
    }
    @media (max-width: 425px) {
      .user-list {
        display: flex;
        flex-direction: column;
        gap: 0px;
      }
    }
    @media (min-width: 426px) and (max-width: 768px) {
      .user-list {
        display: flex;
        flex-direction: column;
        gap: 0px;
      }
    }
    @media (min-width: 769px) and (max-width: 1024px) {
    }
  </style>
  
  <div class="container">
    <p class="header">user list</p>
    <div class="user-list">
      <Userlist/>
    </div>
  </div>
  