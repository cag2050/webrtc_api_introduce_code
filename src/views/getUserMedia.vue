<template>
    <div>
        <video id="video1" autoplay playsinline></video>
    </div>
</template>

<script>
export default {
    mounted() {
        navigator.mediaDevices
            .getUserMedia({
                audio: true,
                video: true
            })
            .then((mediaStream) => {
                let video1 = document.getElementById("video1")
                video1.srcObject = mediaStream
            })
            .catch((err) => {
                console.error(err)
            })
    }
}
</script>

<style scoped></style>
