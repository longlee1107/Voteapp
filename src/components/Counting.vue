<template>
<div>
    <div class="detail">
        {{person.name}} ({{person.counter}})
    </div>
    <div>
        <button class="btn" @click="voteCount()">Vote</button>
    </div>
</div>
</template>

<script>
export default {
    props: {
        person: {
            type: Object,
            default: null,
        },
    },
    data() {
        return{}
    },
    methods: {
        voteCount() {
            this.person.counter++;
            this.$emit("vote", this.person);
        }
    }
}
</script>

<style>
.detail {
    background-color: #FFF;
    padding: 0px 25px 25px 25px;
    margin: 0px -25px -25px;
    font-size: 24px;
    font-weight: 700;
    color: #000000;
}

/* .detail h2{
        margin-bottom: 15px;
    } */
.btn {
    border: none;
    outline: 0;
    padding: 12px;
    color: white;
    background-color: #000;
    text-align: center;
    cursor: pointer;
    width: 100%;
    font-size: 18px;
}

.btn:hover {
    background-color: rgb(255, 0, 0);
}
</style>
