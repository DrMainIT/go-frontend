<script lang="ts">
  import { RouterView } from '@dvcol/svelte-simple-router/components';

  import type { Route, RouterOptions } from '@dvcol/svelte-simple-router/models';
  
  import MainComponent from './components/Main.svelte';
  import AdminComponent from './components/Admin.svelte';
  import ThankYouComponent from './components/ThankYou.svelte';

  const RouteName = {
    Main: 'Main',
    Admin: 'admin',
    ThankYou: 'thankyou',
  } as const;

  type RouteNames = (typeof RouteName)[keyof typeof RouteName];

  export const routes: Readonly<Route<RouteNames>[]> = [
    {
      name: RouteName.Main,
      path: '/',
      component: MainComponent
    },
    {
      name: RouteName.Admin,
      path: `/admin`,
      component: AdminComponent
    },
    {
      name: RouteName.ThankYou,
      path: `/thankyou`,
      component: ThankYouComponent
    },
  ] as const;

  export const options: RouterOptions<RouteNames> = {
    routes,
  } as const;
  
</script>

<RouterView {options} />