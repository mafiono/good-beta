<template>
	<div class="bet-card">
		<div class="onliner"></div>
		<h3>{{ $t('betCard.needAnyHelp') }}</h3>
		<div class="cont-footer-box">
			<img src="../../assets/img/tel.svg" alt="">
			<a href="tel: +420 605 000 888" class="tel">+420 605 000 888</a>
		</div>
		<div class="cont-footer-box">
			<img src="../../assets/img/teleph.svg" alt="">
			<a href="mailto:guest.relation@mail.com" class="mail">guest.relation@mail.com</a>
		</div>
		<router-link tag="a" to="/about" class="btn-cont">{{ $t('betCard.contacts') }}</router-link>
	</div>
</template>