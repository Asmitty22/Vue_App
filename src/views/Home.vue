<template>
  <div class="wrapper">
    <h1 class="titleH">Json Vue API</h1>
    <div class="lineA"></div>
    <div class="userBox">
      <div v-for="user in UserArray" :key="user.id" class="eachUser">
        <h1>{{ user.Name }}</h1>
        <p>{{ user.Email }}</p>
        <!--router-link :to="{ name: 'About', params: {id: 'Austin' } }"><button>Albums</button></router-link-->
         <router-link :to="{ path: 'About/' + user.Id }"><button>Albums</button></router-link>
      </div>
      <router-view/>
    </div>
  </div>
</template>

<script>

export default {
  name: "Home",
  data() {
    let UserArray = [];

    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((json) => {
        for (let i = 0; i <= json.length - 1; i++) {
          let person = {
            Name: json[i].name,
            Email: json[i].email,
            Id: json[i].id,
          };
          UserArray.push(person);
        }
      });

    console.log(UserArray);

    return{UserArray}
  },
};

</script>
<style>
.titleH {
  text-align: center;
}

.lineA {
  height: 5px;
  background: #ec4148;
  width: 90%;
  margin: auto;
}

.wrapper {
  width: 90%;
  background: lightgrey;
  margin: 20px auto;
  border-radius: 15px;
  padding: 10px;
}

.greetings {
  text-align: center;
}
.userBox {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-row-gap: 15px;
  grid-column-gap: 15px;
  margin: 20px auto;
  padding: 10px;
}

.eachUser {
  box-shadow: 0 4px 8px 0 rgb(0 0 0 / 20%), 0 6px 20px 0 rgb(0 0 0 / 19%);
  margin: auto;
  width: 95%;
  height: 100%;
  background: #ec4148;
  color: white;
  text-align: center;
  margin: 15px;
  margin-left: auto;
  margin-right: auto;
}

.eachUser button {
  padding: 10px;
  border-radius: 10px;
  color: white;
  background: #f3ad21;
}
</style>

