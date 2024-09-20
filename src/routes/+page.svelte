  <script>
    import Userlist from "$lib/Userlist.svelte";
  </script>
  <style>
    .header {
      text-transform: uppercase;
      font-weight: 600;
      font-size: 2rem;
      margin-top: 0;
      margin-bottom: 5px;
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
      <p class="header">user list</p>
    </div>
    <div class="row list">
      <Userlist/>
    </div>
  </div>
  