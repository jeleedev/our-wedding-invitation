<script lang="ts">
	import locationDeco from '$lib/assets/location-deco.svg';
	import { _ } from 'svelte-i18n';
	import { localeStore } from '../i18n.svelte';
	import { Clipboard, Github } from '@lucide/svelte';
	import { slide } from 'svelte/transition';

	const googleMapsUrl =
		'https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d6322.860406727866!2d127.035685!3d37.592033!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x357cbcbc8d707a77%3A0x195d6ec549202318!2z6rOg66Ck64yA7ZWZ6rWQIOq1kOyasO2ajOq0gA!5e0!3m2!1sko!2skr!4v1745824760525!5m2!1sko!2skr';

	function copyAddress() {
		navigator.clipboard
			.writeText('서울특별시 성북구 종암동 29-26')
			.then(() => alert($_('서울특별시 성북구 종암동 29-26')))
			.catch(() => null);
	}
</script>

<section class="location">
	<h2 class="title {localeStore.locale}">{$_('location.title')}</h2>
	<p class="venue {localeStore.locale}">웨드유 웨딩 (구.고려스퀘어)</p>
	<button class="copy-address {localeStore.locale}" onclick={copyAddress}>
		<span class="clipboard-icon">
			<Clipboard size="1.1em" />
		</span>
		<span class="address">서울특별시 성북구 종암동 29-26</span></button
	>
	<div class="map">
		<iframe
			class="google-maps"
			title="google maps"
			allowfullscreen
			referrerpolicy="no-referrer-when-downgrade"
			src={googleMapsUrl}
		></iframe>
	</div>
	<div class="content {localeStore.locale}" transition:slide={{ duration: 350 }}>
		<div class="transportation-info">
			<div class="info-group">
				<p class="info-title">지하철</p>
				<p class="info-content">지하철 6호선 고려대역 3번 출구. 직진 도보 3분 내외</p>
			</div>
			<div class="info-group">
				<p class="info-title">버스</p>
				<p class="info-content">정류장명: 고려대학교 앞</p>
				<p class="info-content">간선 101, 144, 173, 273</p>
				<p class="info-content">지선: 111, 1017, 1111, 1222, 2222, 7211</p>
			</div>
			<div class="info-group">
				<p class="info-title">주차</p>
				<p class="info-content">고려대학교 교우회관 주차장 이용 (2시간 무료 주차)</p>
			</div>
		</div>
	</div>
	<p class="signature en">made with ♡ by Ji Eun & Hyo Wook</p>
	<a class="github-icon" href="https://github.com/jeleedev/our-wedding-invitation" target="_blank"
		><Github size="1.1em" strokeWidth={1} /></a
	>
	<img class="location-deco" src={locationDeco} alt="" />
</section>

<style lang="scss">
	section.location {
		position: relative;
		display: flex;
		flex-direction: column;
		align-items: center;
		position: relative;
		background-color: $bg-color-1;
		padding: 1em 2em 1em 2em;
	}

	h2.title {
		color: $primary-color;
		text-align: center;
		margin-bottom: 1em;

		&.kr {
			@extend .title-font-kr;
			letter-spacing: 1px;
		}

		&.en {
			@extend .title-font-en;
			letter-spacing: 1px;
		}
	}

	p.venue {
		&.kr {
			@extend .title-font-kr;
			color: $font-color-default;
			font-size: 1.1rem;
			font-weight: 500;
		}
	}

	button.copy-address {
		display: flex;
		align-items: center;
		margin-top: 0.5em;

		.clipboard-icon {
			height: 1em;
			display: inline-block;
			margin-right: 0.2em;
			color: $font-color-default;
		}

		.address {
			display: inline-block;
			font-size: 0.9rem;
		}
	}

	.map {
		margin-top: 2em;
		width: 100%;
		height: 16em;
		margin-bottom: 2em;
	}

	iframe.google-maps {
		width: 100%;
		height: 100%;
		border: none;
		border-radius: 8px;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
	}

	p.signature {
		font-size: 1rem;
	}
	.github-icon {
		margin-top: 0.2em;
		color: $font-color-default;
		cursor: pointer;
	}

	img.location-deco {
		position: absolute;
		bottom: 1.5em;
		right: 1.5em;
	}

	.transportation-info {
		margin-top: 2em;
		width: 100%;
		margin-bottom: 5em;

		.info-group {
			margin-bottom: 1.5em;

			&:last-child {
				margin-bottom: 0;
			}

			.info-title {
				font-weight: 500;
				margin-bottom: 0.5em;
				color: $font-color-default;
				font-size: 1.1rem;
			}

			.info-content {
				font-size: 0.9rem;
				line-height: 1.5;
				color: $font-color-default;
			}
		}
	}
</style>
