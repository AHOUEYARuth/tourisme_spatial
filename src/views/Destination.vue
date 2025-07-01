<template>
    <main>
        <section id="home">
            <div class="container">
                <div class="content">
                    <p class="p"><strong>01</strong>PICK YOUR DESTINATION</p>   
                    <div class="destination">
                        <div class="img">
                            <img :src="getImageUrl(selectedDestination?.name)" :alt="selectedDestination?.name" />
                        </div>
                        <nav>
                            <ul>
                                <li v-for="(destination, index) in destinationData" :key="index"
                                    @click="selectDestination(destination)"
                                    :class="{ active: destination.name === selectedDestination?.name }">
                                    {{ destination.name.toUpperCase() }}
                                </li>
                            </ul>
                            <div class="div">
                                <h1>{{ selectedDestination?.name }}</h1>
                                <p>{{ selectedDestination?.description }}</p>
                                <div class="bar"></div>
                                <div class="foot">
                                    <div class="distance">
                                        <p>AVG. DISTANCE</p>
                                        <h3>{{ selectedDestination?.distance }}</h3>
                                    </div>
                                    <div class="time">
                                        <p>Est. travel time</p>
                                        <h3>{{ selectedDestination?.travel }}</h3>
                                    </div>
                                </div>
                            </div>
                        </nav>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>

<script setup lang="ts">
import axios from "axios";
import { ref, onMounted } from "vue";

const destinationData : any = ref([]);
const selectedDestination: any = ref(null);

// Dynamically import all destination images
const images = import.meta.glob('../assets/destination/image-*.png', { eager: true, import: 'default' });

function getImageUrl(name: string | undefined): string {
    if (!name) return '';
    const key = `../assets/destination/image-${name.toLowerCase()}.png`;
    const img = images[key];
    // If img is a string, return it; if it's a module/object, try to get its default export
    if (typeof img === 'string') return img;
    if (img && typeof img === 'object' && 'default' in img) return img.default as string;
    return '';
}

onMounted(async () => {
    const response = await axios.get('/data.json');
    destinationData.value = response.data.destinations;

    selectedDestination.value = destinationData.value[1];
    console.log('Destinations:', destinationData.value);
});

const selectDestination = (destination: any) => {
    console.log(destination);
    
    selectedDestination.value = destination;
};
</script>

<style scoped>
main {
    color: #fff;
}

#home {
    width: 100%;
    background-image: url(/src/assets/destination/background-destination-desktop.jpg);
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
    min-height: calc(100vh - 92px);
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 60px;
    padding-top: 92px;
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

.destination {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
}

.destination img {
    width: 80%;
}

ul {
    display: flex;
    align-items: center;
    gap: 40px;
}

li {
    list-style: none;
    color: #ffffffcc;
    cursor: pointer;
}

.active {
    color: #ffffff;
    border-bottom: 2px solid #ffffff;
}

.div {
    width: 380px;
    padding: 10px 40px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    height: 100%;
}

.bar {
    width: 100%;
    height: 1px;
    background-color: #ffffff49;
}

.foot {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.div h1,
.div p,
.div .bar,
.div .foot {
    margin: 0;
}

.div h1 {
    font-weight: 5;
    font-size: 80px;
}

.div p,
.foot p {
    color: #ffffffb4;
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

    #home {
        background: url(/src/assets/destination/background-destination-tablet.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
    }

    .destination {
        display: flex;
        flex-direction: column-reverse;
        gap: 20px;
        width: 100%;
        text-align: center;
    }

}

@media screen and (max-width: 375px) {
    main {
        width: 100%;
        overflow-x: hidden;
    }

    #home {
        background: url(/src/assets/destination/background-destination-mobile.jpg);
        background-size: cover;
        min-width: 100%;
        background-repeat: no-repeat;
        /* height: 100%; */
    }

    .container {
        max-width: 80%;
        margin: 0 auto;
    }

    .content {
        width: 100%;
    }

    .content p {
        font-size: 13px;
        gap: 5px;
    }

    ul {
        flex-wrap: wrap;
        width: 100%;
        gap: 25px;
        padding: 0;
    }

    nav {
        width: 100%;
    }

    .div {
        width: 100%;
        text-align: center;
        padding: 0;
    }

    .div h1 {
        font-size: 40px;
    }

    .div p {
        font-size: 16px;
    }
}
</style>