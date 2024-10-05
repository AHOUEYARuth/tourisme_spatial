<template>
    <main>
        <section id="technologie">
            <div class="container">
                <div class="content">
                    <p class="p"><strong>03</strong>SPACE LOUNCH 101</p>
                    <div class="techno_content">
                        <nav>
                            <ul>
                                <li class="btn" v-for="(technology, index) in technologyData" :key="index"
                                    @click="selectT(technology)"
                                    :class="{ active: technology.name === selectedT?.name }">{{ index + 1 }}</li>
                            </ul>
                            <div class="text">
                                <p>THE TECHNOLOGY...</p>
                                <h1>{{ selectedT?.name.toUpperCase() }}</h1>
                                <P>{{ selectedT?.description }}</P>
                            </div>
                        </nav>
                        <div class="img"><img :src="selectedT?.images.portrait" alt="">
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>


<script setup lang="ts">
import axios from "axios";
import { ref, onMounted } from "vue";

const technologyData = ref([])
const selectedT = ref(null)

onMounted(async () => {
    const response = await axios.get('/data.json');
    technologyData.value = response.data.technology;

    selectedT.value = technologyData.value[0];
    console.log('Technology:', technologyData.value);
});
const selectT = (technology: any) => {
    selectedT.value = technology;
};
</script>


<style scoped>
main {
    color: #fff;
}

#technologie {
    width: 100%;
    background-image: url(/src/assets/technology/background-technology-desktop.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    padding: 0;
    margin: 0;
}

.container {
    max-width: 1044px;
    margin: 0 auto;
}

.content {
    width: 100%;
    display: flex;
    min-height: calc(100vh - 92px);
    flex-direction: column;
    justify-content: center;
    padding-top: 92px;
    gap: 20px;
}

nav {
    display: flex;
    align-items: center;
    gap: 50px;
    width: 600px;
    padding: 0;
}

.p,
nav p {
    display: flex;
    gap: 20px;
    font-size: 18px;
    align-items: center;
    letter-spacing: 5px;
    margin: 0;
}

.p strong {
    color: #ffffff79;
}

nav p {
    color: #ffffffb6;
    margin: 10px;
}

ul {
    padding: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
    margin: 0;
    gap: 40px;
}

li {
    list-style: none;
}

.techno_content {
    width: 100%;
    display: flex;
    align-items: center;
    gap: 80px;
}

.btn {
    width: 60px;
    height: 60px;
    border-radius: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    border: 1px solid rgb(151, 151, 151);
    font-size: 18px;
}

.img img {
    width: 80%;
    border-radius: 15px;
}

h1 {
    font-weight: 5;
    font-size: 40px;
    margin: 5px;
}

.active {
    background-color: #fff;
    border: none;
    color: #000;
}

.text {
    width: 90%;
}

.text p {
    font-size: 16px;
    font-family: "Khand", sans-serif;
}

@media screen and (max-width: 1024px) {
    body {
        width: 100%;
    }

    .header {
        width: 100%;
    }

    .container {
        max-width: 80%;
    }

    h1 {
        font-size: 30px;
    }

    .text p {
        font-size: 14px;
    }
}

@media screen and (max-width: 768px) {
    body {
        width: 100%;
    }

    .header {
        width: 100%;
    }

    .container {
        max-width: 80%;
    }

    .content {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 20px;
        padding-top: 120px;
        padding-bottom: 50px;
    }

    #technologie {
        background: url(/src/assets/technology/background-technology-tablet.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
    }

    .techno_content {
        display: flex;
        flex-direction: column-reverse;
        gap: 20px;
        width: 100%;
        text-align: center;
    }

    .text {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    nav{
        display: flex;
        flex-direction: column-reverse;
    }
    ul{
        display: flex;
        flex-direction: row;
    }
}
@media screen and (max-width: 375px) {
    main{
        width: 100%;
    }
    #technologie{
        background-image: url(/src/assets/technology/background-technology-mobile.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
    }
    .container {
        max-width: 80%;
        margin: 0 auto;
    }
    .content{
        padding-bottom: 30px;
    }
    .techno_content {
        display: flex;
        flex-direction: column-reverse;
        gap: 20px;
        width: 100%;
        text-align: center;
    }
    .content p {
        font-size: 17px;
        gap: 5px;
    }
    nav{
        width: 100%;
    }
    .text{
        width: 100%;
        padding: 0;
    }
}

</style>