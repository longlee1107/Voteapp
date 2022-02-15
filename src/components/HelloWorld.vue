<template>
<div>
    <div>
        <div style="width:50%; float:left; display: flex; align-items: center; justify-content: center; margin-left:80px">
            <div class="rank3">
                <h3>Top 3</h3>
                <img :src="this.third.src" alt="image" />
                <h2>{{this.third.name}}</h2>
                <h4>Vote: {{this.third.counter}}</h4>
            </div>
            <div class="rank1">
                <h3>Top 1</h3>
                <img :src="this.first.src" alt="image" />
                <h2>{{this.first.name}}</h2>
                <h4>Vote: {{this.first.counter}}</h4>
            </div>
            <div class="rank2">
                <h3>Top 2</h3>
                <img :src="this.second.src" alt="image" />
                <h2>{{this.second.name}}</h2>
                <h4>Vote: {{this.second.counter}}</h4>
            </div>
        </div>
        <div class="voteHistory">
            <h5>Vote History</h5>
            <ul>
                <li v-for="data in history" :key="data.index">
                    You voted for:<span style="color: blue">{{data.name}}</span>
                </li>
            </ul>

        </div>
    </div>
    <div v-for="person in renderList" :key="person.id" style="flex: 1 1 33.333%; width: 300px; padding: 25px; display: inline-block;">
        <div :class="'list-inner'">
            <div class="list-image-wrap">
                <img :src="person.src" class="image" />
            </div>
            <div class="list-detail">
                <Counting :person="person" @vote="onVote" />
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Counting from "../components/Counting.vue"
export default {
    name: 'HelloWorld',
    components: {
        Counting
    },
    data() {
        return {
            renderList: [],
            history: [],
            peoples: [{
                    id: 1,
                    name: 'Nike',
                    counter: 0,
                    src: 'https://i.pinimg.com/236x/e5/cf/66/e5cf66cf4afaf85d092b9f02509e440e.jpg'
                },
                {
                    id: 2,
                    name: 'Nikel',
                    counter: 0,
                    src: 'https://www.dogalize.com/wp-content/uploads/2017/05/funny-cat-img-200x200.jpg'
                },
                {
                    id: 3,
                    name: 'Runs',
                    counter: 0,
                    src: 'https://i.pinimg.com/474x/02/34/bd/0234bd2da5a29016c7f82e8fa5669781.jpg'
                },
                {
                    id: 4,
                    name: 'Nikex',
                    counter: 0,
                    src: 'https://i.pinimg.com/originals/a9/39/52/a93952379d9b4f44e413df0118e57b1b.jpg'
                },
                {
                    id: 5,
                    name: 'Sux',
                    counter: 0,
                    src: 'https://i.pinimg.com/originals/00/d7/59/00d759aeb06c81fff12790b8ddacc50a.jpg'
                },
            ],
            first: {
                id: 0,
                name: '',
                counter: 0,
                src: '',
            },
            second: {
                id: 0,
                name: '',
                counter: 0,
                src: '',
            },
            third: {
                id: 0,
                name: '',
                counter: 0,
                src: '',
            },
        }
    },
    created() {
        this.useCookies();
        this.renderList = Object.assign([], this.peoples)
        this.topRank();
    },
    watch: {
        peoples: {
          handler() {
            // this.topRank();
            this.setCookies("onVote", JSON.stringify(this.renderList), 1);
          },
          deep: true,
        },
    },
    methods: {
        onVote(data) {
            // this.getCookies();
            this.topRank(),
            this.history.push(data)
        },
        setCookies(keyname,keyvalue,extime){
            let d = new Date();
            d.setTime(d.getTime()+ extime*1*24*60*1000);
            let expires = "expires=" +d.toUTCString();
            document.cookie = keyname + "=" + keyvalue + ";" + expires + ";path=/";
        },

        getCookies(keyname){
            let name = keyname + "=";
            let dCookie = decodeURIComponent(document.cookie);
            let x = dCookie.split(";");
            for (let i = 0; i < x.length; i++) {
        let c = x[i];
        while (c.charAt(0) == " ") {
          c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
          return c.substring(name.length, c.length);
        }
      }
      return "";
    },
    useCookies(){
      if(this.getCookies("onVote") != ''){
        this.peoples = JSON.parse(this.getCookies("onVote"));
      }
    },
        topRank() {
            const arr = this.peoples.sort(function (a, b) {
                return b.counter - a.counter
            });
            this.first = arr[0];
            this.second = arr[1];
            this.third = arr[2];
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>
.list-inner {
    position: relative;
    padding: 25px;
    box-shadow: 0 0 16px black;
    border-radius: 15px;
    perspective: 1000px;
}

.list-image-wrap {
    position: relative;
    z-index: 1;
    transform-origin: center;
}

.list-image-wrap .image {
    width: 100%;
    filter: drop-shadow(0px 0px 12px rgba(0, 0, 0, 0.25));
}

.list-detail {
    background-color: #FFF;
    padding: 25px;
    margin: 0px -25px -25px;
}

.list-detail h2 {
    font-size: 24px;
    font-weight: 700;
    color: #000000;
    margin-bottom: 15px;
}
.rank1, .rank2, .rank3{
    border-radius: 10px;
}
.rank1 {
    height: 400px;
    width: 250px;
    margin: 10px;
    border: 1px solid black;
    color: blueviolet;
    padding: 10px;
}

.rank2 {
    margin: 10px;
    padding: 10px;
    height: 350px;
    width: 200px;
    color: blue;
    border: 1px solid black;
}

.rank3 {
    margin: 5px 10px 10px 10px;
    padding: 10px 10px 10px 10px;
    height: 300px;
    width: 200px;
    color: rgb(247, 92, 92);
    border: 1px solid black;
}

img {
    width: 75%;
    height: auto;
    border-radius: 5px;
}

.voteHistory {
    display: flex;
    /* justify-content: center; */
    flex-direction: column;
    border: 5px solid black;
    border-radius: 10px;
    height: 500px;
    width: 400px;
}
.voteHistory h5{
color:rgb(255, 0, 0);
  font-size: 24px;
  font-weight: 700;
  text-decoration: underline;
}
.voteHistory ul{
  font-size: 20px;
  font-weight: 500;
  list-style: none;
  overflow: auto;
  padding-left: 0;
}


</style>
