<template>
  <section class="content mb-2">
    <h2>Routes</h2>
    <nav
      class="navbar navbar-expand-xl navbar-dark bg-dark"
      style="background-color: #e3f2fd"
    >
      <ul>
        <li class="nav-item">
          <router-link to="/form">
            <a class="nav-link" href="#">Form</a>
          </router-link>
        </li>

        <li class="nav-item">
          <router-link to="/requests">
            <a class="nav-link" href="#">Requests</a>
          </router-link>
        </li>
      </ul>
    </nav>
  </section>
</template>

<script>
export default {
  name: "routes-view",
};
</script>

<style>
section nav ul {
  width: 100%;
  padding: 5px;
  margin: 0;
  display: flex;
  justify-content: center;
  row-gap: 5px;
  font-size: 1.2rem;
  font-weight: 700;
  list-style: none;
  color: white;
}

section nav ul li a {
  border-radius: 5px;
  background-color: rgb(50, 4, 187);
  color: white;
}

section nav ul li a:hover {
  color: black;
  text-decoration: none;
}
</style>