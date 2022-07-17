<template>
    <div id="nav">
        <router-link to="/">Home</router-link>
        |
        <router-link to="/getUserMedia">getUserMedia()：获取摄像头和麦克风</router-link>
        |
        <router-link to="/enumerateDevices">enumerateDevices()：查询媒体设备</router-link>
        |
        <router-link to="/getDisplayMedia">getDisplayMedia()：屏幕分享</router-link>
        |
        <router-link to="/PeerConnectionCanvas">白板示例</router-link>
        |
    </div>
    <router-view />
</template>

<style lang="less">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: left;
    color: #2c3e50;
}

#nav {
    //padding: 30px;

    a {
        font-weight: bold;
        color: #2c3e50;

        &.router-link-exact-active {
            color: #42b983;
        }
    }
}
</style>
