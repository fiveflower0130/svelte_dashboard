<script>
  import MDBNavbar from 'mdbsvelte/src/MDBNavbar.svelte';
  import MDBNavbarBrand from 'mdbsvelte/src/MDBNavbarBrand.svelte';
  import MDBNavbarNav from 'mdbsvelte/src/MDBNavbarNav.svelte';
  import MDBNavbarToggler from 'mdbsvelte/src/MDBNavbarToggler.svelte';
  import MDBCollapse from 'mdbsvelte/src/MDBCollapse.svelte';
  import MDBNavItem from 'mdbsvelte/src/MDBNavItem.svelte';
  import MDBNavLink from 'mdbsvelte/src/MDBNavLink.svelte';
  import MDBIcon from 'mdbsvelte/src/MDBIcon.svelte';

  let collapse = false;
  function toggle() {
    collapse = !collapse;
  }

  function handleUpdate(event) {
    collapse = event.detail.isOpen;
  }
</script>

<MDBNavbar class="flexible-navbar" light expand="md">
  <MDBNavbarBrand href="/">
    <strong>CTRD</strong>
  </MDBNavbarBrand>
  <MDBNavbarToggler on:click={toggle} />
  <MDBCollapse isOpen={collapse} navbar expand="md" on:update={handleUpdate}>
    <MDBNavbarNav left>
      <MDBNavItem>
        <MDBNavLink to="#">Home</MDBNavLink>
      </MDBNavItem>
    </MDBNavbarNav>
    <MDBNavbarNav right>
      <!-- <MDBNavItem>
        <a
          class="nav-link navbar-link"
          rel="noopener noreferrer"
          target="_blank"
          href="https://pl-pl.facebook.com/mdbootstrap/"
          ><MDBIcon fab icon="facebook" /></a
        >
      </MDBNavItem>
      <MDBNavItem>
        <a
          class="nav-link navbar-link"
          rel="noopener noreferrer"
          target="_blank"
          href="https://twitter.com/mdbootstrap"
          ><MDBIcon fab icon="twitter" /></a
        >
      </MDBNavItem> -->
      <MDBNavItem>
        <a
          class="border border-light rounded mr-1 nav-link Ripple-parent"
          rel="noopener noreferrer"
          href="https://github.com/SauravKanchan/mdbsvelte-dashboard"
          target="_blank"><MDBIcon fab icon="github" class="mr-2" />K09857</a
        >
      </MDBNavItem>
      <MDBNavItem>
        <a
          class="border border-light rounded mr-1 nav-link Ripple-parent"
          rel="noopener noreferrer"
          href="https://github.com/SauravKanchan/mdbsvelte"
          target="_blank"><MDBIcon fas icon="door-open" class="mr-2" />LOGOUT</a
        >
      </MDBNavItem>
    </MDBNavbarNav>
  </MDBCollapse>
</MDBNavbar>
