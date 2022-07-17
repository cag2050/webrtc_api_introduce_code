<template>
    <div>{{ deviceInfos }}</div>
</template>

<script>
export default {
    data() {
        return {
            deviceInfos: []
        }
    },
    mounted() {
        navigator.mediaDevices
            .enumerateDevices()
            .then((deviceInfos) => {
                this.deviceInfos = deviceInfos
                deviceInfos.forEach((deviceInfo) => {
                    console.log(deviceInfo.toJSON())
                })
            })
            .catch((err) => {
                console.error(err)
            })
    }
}
</script>

<style scoped></style>
