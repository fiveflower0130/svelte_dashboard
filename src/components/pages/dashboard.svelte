<script>
  import AdminCardSection1 from './sections/AdminCardSection1.svelte';
  import AdminCardSection2 from './sections/AdminCardSection2.svelte';
  import BreadcrumbSection from './sections/BreadcrumbSection.svelte';
  import ChartSection1 from './sections/ChartSection1.svelte';
  import ChartSection2 from './sections/ChartSection2.svelte';
  import TableSection1 from './sections/TableSection1.svelte';
  import TableSection2 from './sections/TableSection2.svelte';
  import ModalSection from './sections/ModalSection.svelte';
  import MDBContainer from 'mdbsvelte/src/MDBContainer.svelte';
</script>

<MDBContainer fluid>
  <BreadcrumbSection />
  <!--<AdminCardSection1 /> -->
  <ChartSection1 />
  <TableSection1 />
  <ChartSection2 />
  <TableSection2 />
  <!-- <ModalSection />
  <AdminCardSection2 /> -->
</MDBContainer>
