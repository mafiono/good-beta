<template>
	<div class="mini-chat">
		<div class="chat-box" v-for="mes in loadMessages" @click="openMessage(mes)">
			<p>{{mes.title}}</p>
			<p class="small-white" v-html="mes.message.substr(0, 38) + '...' "></p>
			<div class="onliner" v-if="mes.status === 'delivered' "></div>
		</div>
	</div>
</template>


<script>
import {mapGetters} from 'vuex'

export default{
	props: {
    openButton: {
			type: HTMLDivElement
		}
	},
	computed: {
		...mapGetters({
        loadMessages: "messages/getMessages",
			}),
	},
  mounted() {
    let allApp = document.querySelector('#app')

    allApp.addEventListener('click', (e) => {
      if (!this.$el.contains(e.target) && !e.target.contains(this.openButton)) {
        this.$emit('closeMiniChat')
      }
    })
  },
  created() {
    this.$store.dispatch('messages/loadMessages')
  },
  methods: {
    openMessage(message){
			this.$emit('openMessage', message)
      this.$store.dispatch('message/setUnreadByMessageId', message.id)
		}
	}
}
</script>


<style>
.mini-chat{
	position: absolute;
	top: 70px;
	background-color: #0d0d25;
	border-radius:5px;
	height: 200px;
	overflow-y:scroll;
	width: 300px;
	padding: 10px;
}
.chat-box{
	margin-bottom: 10px;
	padding:5px 10px;
	cursor: pointer;
	transition: all .3s ease;
	border-radius: 5px;
	text-transform: none!important;
	position: relative;
}
.chat-box:hover{
	background-color: #272459;
}
.chat-box:before{
	content: '';
	width: calc(100% - 20px);
	height: 1px;
	background-color: #fff;
	opacity: 0.4;
	left: 10px;
	bottom: -2px;
	position: absolute;
}
.chat-box:hover::before{
	display: none;
}
.chat-box:last-child::before{
	display: none;
}
</style>