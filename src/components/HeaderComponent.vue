<template>

  <header class="container">
    <div class="header-left">
      <div class="header-img">
        <img src="../assets/img/netflix-logo-png-2562.png" alt="netflix logo">
      </div>
      <nav>
        <ul>
          <li>bla</li>
          <li>bla</li>
          <li>bla</li>
          <li>bla</li>
          <li>bla</li>
        </ul>
      </nav>
    </div>
    <div class="header-right">
      <input type="text">
    </div>

  </header>


</template>
<script>
export default {
  name: 'HeaderComponent'
}
</script>
<style scoped lang="scss">
@import '../index.scss';

 .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;

  & .header-left {
    display: flex;
    align-items: center;

    & ul {
      display: flex;
      color: white;
      gap: 15px;

    }
  }

  & .header-right {
    border-radius: 10px;
  }
}

.header-img {
  max-width: 150px;
  margin-right: 50px;

}
</style>