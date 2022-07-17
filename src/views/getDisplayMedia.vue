<template>
    <div>
        <div>
            <button @click="startScreenShare">开始屏幕分享</button>
            <button @click="closeScreenShare" style="margin-left: 20px">结束屏幕分享</button>
        </div>
        <div>
            <video id="video1" autoplay playsinline></video>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            mediaStream: null
        }
    },
    mounted() {},
    methods: {
        startScreenShare() {
            navigator.mediaDevices
                .getDisplayMedia({
                    video: true,
                    audio: true // 添加此行时，【选择要分享什么】窗口的【Chrome标签页】tab下面会有一个单选框【分享标签页中的音频】；如果选择此单选框，会有2个track
                })
                .then((mediaStream) => {
                    console.log(mediaStream)
                    this.mediaStream = mediaStream
                    let video1 = document.getElementById("video1")
                    video1.srcObject = mediaStream

                    // 点击漂浮栏中的【停止共享】按钮，MediaStream 触发 oninactive 事件，同时 MediaStreamTrack 触发 onended 事件
                    mediaStream.oninactive = () => {
                        console.log("mediaStream oninactive")
                    }

                    mediaStream.getTracks().forEach((track) => {
                        console.log("track:", track)
                    })
                    if (mediaStream.getAudioTracks().length > 0) {
                        let audioTrack = mediaStream.getAudioTracks()[0]
                        audioTrack.onended = () => {
                            console.log("audio track onended")
                        }
                    }
                    if (mediaStream.getVideoTracks().length > 0) {
                        let videoTrack = mediaStream.getVideoTracks()[0]
                        videoTrack.onended = () => {
                            console.log("video track onended")
                        }
                    }
                })
                .catch((err) => {
                    console.log(typeof err)
                    console.log(err)
                })
        },
        closeScreenShare() {
            // MediaStream 中所有的 track，都stop()后，【停止共享】所在的漂浮栏消失
            if (this.mediaStream?.getAudioTracks().length > 0) {
                console.log("audio track stop()")
                this.mediaStream?.getAudioTracks()[0].stop()
            }
            if (this.mediaStream.getVideoTracks().length > 0) {
                console.log("video track stop()")
                this.mediaStream?.getVideoTracks()[0].stop()
            }
        }
    }
}
</script>

<style scoped></style>
