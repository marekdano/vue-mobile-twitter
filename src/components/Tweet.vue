<template>
	<div class="tweet">
		<article class="media">
			<figure class="media-left">
				<p class="image is-64x64">
					<img class="user-image" :src="tweet.userImage">
				</p>
			</figure>
			<div class="media-content">
				<div class="content">
					<p>
						<strong>{{tweet.name}}</strong>
						<img class="verified-icon"
									src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/twitter_verified.png"
									v-if="tweet.verified" />
						<small>{{tweet.handle}}</small>
						<small class="time-lapsed">{{tweet.timeLapsed}}</small>
						<br>
						<span class="description" v-html="computedDescription"></span>
					</p>
				</div>
				<div v-if="tweet.tweetImage" class="tweet-image">
					<img :src="tweet.tweetImage" />
				</div>
				<nav class="level is-mobile">
					<div class="level-left">
						<a class="level-item">
							<span class="icon is-small"><i class="far fa-comment"></i></span>
						</a>
						<a class="level-item">
							<span class="icon is-small"><i class="fas fa-retweet"></i></span>
						</a>
						<a class="level-item heart" @click="like">
							<span class="icon is-small">
								<i class="far fa-heart"
										:class="{'fas': this.tweet.upVoted}"></i>
							</span>
							<p :class="{'bold': this.tweet.upVoted}">
								{{new Intl.NumberFormat().format(tweet.likes)}}
							</p>
						</a>
					</div>
				</nav>
			</div>
		</article>
  </div>
</template>

<script>
	export default {
  	name: 'tweet',
		props: ['tweet'],
		computed: {
			computedDescription() {
				return this.tweet.description.split(' ').map((word) => {
					if (word[0] === '@' || word[0] === '#') {
						word = `<span class="highlighted">${word}</span>`;
					}
					return word;
				}).join(' ');
			}
		},
		methods: {
			like() {
				this.tweet.upVoted ? this.tweet.likes-- : this.tweet.likes++;
				this.tweet.upVoted = !this.tweet.upVoted;
			}
		}
	}
</script>

