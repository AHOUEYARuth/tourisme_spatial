<template>
    <main>
        <section id="crew">
            <div class="container">
                <div class="content">
                    <p class="p"><strong>02</strong>MEET OUR CREW</p>
                    <div class="crew">
                        <div class="description">
                            <ul>
                                <li v-for="(crew, index) in crewData" :key="index" @click="selectCrew(crew)"
                                    :class="{ active: crew.name === selectedCrew?.name }"></li>
                            </ul>
                            <div class="info">
                                <h3>{{ selectedCrew?.role.toUpperCase() }}</h3>
                                <h1>{{ selectedCrew?.name.toUpperCase() }}</h1>
                                <p class="p">{{ selectedCrew?.bio }}</p>
                            </div>
                        </div>
                        <div class="img"><img :src="getImageUrl(selectedCrew?.name)" alt=""></div>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>


<script setup lang="ts">
import axios from "axios";
import { ref, onMounted } from "vue";

interface CrewMember {
    name: string;
    role: string;
    bio: string;
    images: {
        png: string;
        webp: string;
    };
}

const crewData = ref<CrewMember[]>([])
const selectedCrew = ref<CrewMember | null>(null)

const images = import.meta.glob('../assets/crew/image-*.png', { eager: true, import: 'default' });
function getImageUrl(name: string | undefined): string {
    if (!name) return '';

    const key = `../assets/crew/image-${name.toLowerCase().split(" ").join('-')}.png`;
    const img = images[key];
    if (typeof img === 'string') return img;
    if (img && typeof img === 'object' && 'default' in img) return img.default as string;
    return '';
}


onMounted(async () => {
    const response = await axios.get('/data.json');
    crewData.value = response.data.crew;

    selectedCrew.value = crewData.value[3];
    console.log('Crews:', crewData.value);
});

const selectCrew = (crew: any) => {
    selectedCrew.value = crew;
};
</script>


<style scoped>
main {
    color: #fff;
}

#crew {
    width: 100%;
    background-image: url(/src/assets/crew/background-crew-desktop.jpg);
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
    /*    padding: 90px 0;
 */
    /*  gap: 30px; */
}

.p {
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

.crew {
    width: 100%;
   /*  height: 100%; */
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0;
}
.crew img {
    width: 70%;
    height: 100%;
}

ul {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 0;
}

li {
    list-style: none;
    width: 10px;
    height: 10px;
    border: 1px solid rgb(187, 184, 184);
    border-radius: 30px;
}

.description {
    width: 450px;
    height: 350px;
    display: flex;
    flex-direction: column-reverse;
    justify-content: space-between;
    /* gap: 150px; */
}

.info {
    height: 50%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

h1,
h3 {
    font-weight: 5;
}

h3,
.p {
    color: #ffffffab;
}

.active {
    background-color: #fff;
}

@media screen and (max-width: 1024px) {
    body {
        width: 100%;
    }

    .main {
        width: 100%;
        height: 100%;
        overflow-y: visible;
        background-color: #ffffff;
    }

    .container {
        max-width: 80%;
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
    }

    #crew {
        background: url(/src/assets/crew/background-crew-tablet.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
    }

    .crew {
        display: flex;
        flex-direction: column-reverse;
        gap: 20px;
        width: 100%;
        text-align: center;
    }
    .description{
        width: 100%;
        text-align: center;
        justify-content: space-between;
        
    }
    ul{
        justify-content: center;
    }
}
@media screen and (max-width: 375px) {
    main{
        width: 100%;
    }
    #crew{
        background-image: url(/src/assets/crew/background-crew-mobile.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
    }
    .content{
        padding-bottom: 30px;
    }
    .description{
        display: flex;
        flex-direction: column-reverse;
        justify-content: space-between;
        height: 400px;
    }
    .info p{
        font-size: 15px;
    }
}
</style>