<template>
	<header id="masthead" class="site-header" role="banner">

		<div class="row">

			<div class="column medium-2 hide-for-small-only">

				<router-link :to="{ name: 'home'}" class="site-name"> {{ site_name }} </router-link>

			</div>

			<div class="column medium-10">

				<a id="primary-nav-button" class="menu-toggle" data-toggle="offCanvasLeft" >
					<!--Menu Icon here-->
					<div>&#9776;</div>
				</a>

				<div class="off-canvas position-left" id="offCanvas" data-off-canvas >
					<!-- Your menu or Off-canvas content goes here -->

				<nav id="site-navigation">

					<ul>
						<li v-for="item in menus" v-if="item.type != 'custom'">
							 <router-link :to="{ name: 'page', params: { name: getUrlName( item.url ) }}"> {{ item.title }} </router-link>
						</li>
					</ul>

				</nav>
				</div>
			</div>

		</div>

	</header>

</template>

<script>
export default {

	mounted: function () {

		//console.log( wp.api.collections );
		this.getMenu();
	},
	data() {
		return {
			menus: [],
			site_name: rtwp.site_name,
		}
	},
	methods: {

		getMenu: function () {

			var vm = this;

			vm.$http.get( 'wp-api-menus/v2/menu-locations/primary-menu')
			.then( (res) => {
				vm.menus = res.data;
			} )
			.catch( (res) => {
				console( `Something wen wrong : ${res}` );
			})

		},
		getUrlName:function( url ) {

			var array = url.split('/');
			var lastsegment = array[array.length-2];
			return lastsegment;
		}


	}

}
</script>

<style>

</style>
