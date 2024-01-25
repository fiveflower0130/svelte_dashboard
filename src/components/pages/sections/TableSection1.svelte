<script>
  import MDBCard from 'mdbsvelte/src/MDBCard.svelte';
  import MDBCardBody from 'mdbsvelte/src/MDBCardBody.svelte';
  import MDBCardHeader from 'mdbsvelte/src/MDBCardHeader.svelte';
  import MDBRow from 'mdbsvelte/src/MDBRow.svelte';
  import MDBCol from 'mdbsvelte/src/MDBCol.svelte';
  import MDBTable from 'mdbsvelte/src/MDBTable.svelte';
  import MDBTableHead from 'mdbsvelte/src/MDBTableHead.svelte';
  import MDBTableBody from 'mdbsvelte/src/MDBTableBody.svelte';
  import {onMount} from 'svelte';
  import {read, utils} from 'xlsx';

  let pres = [];

  onMount(() => {
    const loadData = async () => {
      const response = await fetch('https://sheetjs.com/pres.xlsx');
      const arrayBuffer = await response.arrayBuffer();
      // const filePath = path.resolve('C:/Download/pres.xlsx');
      // const buffer = fs.readFileSync(filePath);
      const workbook = read(arrayBuffer, {type: 'buffer'});
      const worksheet = workbook.Sheets[workbook.SheetNames[0]];
      pres = utils.sheet_to_json(worksheet);
    };

    // Load data immediately on mount
    loadData();

    // Then load data every 10 minutes
    setInterval(loadData, 600000);
  });
</script>

<MDBRow class="mb-4">
  <MDBCol md="12">
    <MDBCard>
      <MDBCardHeader>重要客戶工程批表</MDBCardHeader>
      <MDBCardBody>
        <MDBTable responsive hover>
          <MDBTableHead color="light-blue lighten-4">
            <tr>
              <th>NO.</th>
              <th>Customer</th>
              <th>Device</th>
              <th>Schedule</th>
              <th>SOD</th>
              <th>Status 燈號</th>
              <th>憑單日過站數</th>
              <th>應過站數(SOD基準)</th>
              <th>Status 燈號(P-S)</th>
              <th>MES Stage Code</th>
            </tr>
          </MDBTableHead>
          <MDBTableBody>
            {#each pres as item, i}
              <tr>
                <td>{i + 1}</td>
                <td>
                  <div class="d-flex align-items-center">
                    <img
                      src="intel.png"
                      alt=""
                      style="width: 50px; height: 40px"
                      class="rounded-circle"
                    />
                    <div class="ms-3">
                      <p class="fw-bold mb-1">{item.Name}</p>
                      <p class="text-muted mb-0">
                        UBM PR Thickness and Opening Measurement
                      </p>
                    </div>
                  </div>
                </td>
                <td>{item.Index}</td>
                <td>32IEQVB002</td>
                <td>11/11</td>
                <td>
                  <span class="badge badge-success rounded-pill d-inline"
                    >Active</span
                  >
                </td>
                <td>0.506</td>
                <td>1.207</td>
                <td>(0.7)</td>
                <td>6547</td>
              </tr>
            {/each}
            <!-- <tr>
              <td>1</td>
              <td>Mark</td>
              <td>Otto</td>
              <td>@mdo</td>
            </tr>
            <tr>
              <td>2</td>
              <td>Jacob</td>
              <td>Thornton</td>
              <td>@fat</td>
            </tr>
            <tr>
              <td>3</td>
              <td>Larry</td>
              <td>the Bird</td>
              <td>@twitter</td>
            </tr> -->
          </MDBTableBody>
        </MDBTable>
      </MDBCardBody>
    </MDBCard>
  </MDBCol>
  <!-- <MDBCol md="6" class="mb-4">
    <MDBCard>
      <MDBCardBody>
        <MDBTable responsive hover>
          <MDBTableHead color="blue lighten-4">
            <tr>
              <th>#</th>
              <th>First</th>
              <th>Last</th>
              <th>Handle</th>
            </tr>
          </MDBTableHead>
          <MDBTableBody>
            <tr>
              <td>1</td>
              <td>Mark</td>
              <td>Otto</td>
              <td>@mdo</td>
            </tr>
            <tr>
              <td>2</td>
              <td>Jacob</td>
              <td>Thornton</td>
              <td>@fat</td>
            </tr>
            <tr>
              <td>3</td>
              <td>Larry</td>
              <td>the Bird</td>
              <td>@twitter</td>
            </tr>
          </MDBTableBody>
        </MDBTable>
      </MDBCardBody>
    </MDBCard>
  </MDBCol> -->
</MDBRow>
