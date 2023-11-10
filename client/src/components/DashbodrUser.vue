<template>
  <div class="show">
    <div class="header-title-wrapper">
        <label for="menu-toggle">
          <span class="bx bx-menu"></span>
        </label>
        <div class="header-title">
          <h1>Dashboard</h1>
        </div>
      </div>
    <main>
      <section>
        <h3 class="section-head">Mes Heures</h3>
        <div class="analystics">
          <div class="analystic">
            <div class="analystic-icon">
              <span class="bx bx-low-vision"></span>
            </div>
            <div class="analystic-info">
              <h4>la journée</h4>
              <h1>0(hrs)</h1>
            </div>
          </div>
          <div class="analystic">
            <div class="analystic-icon">
              <span class="bx bx-low-vision"></span>
            </div>
            <div class="analystic-info">
              <h4>la semaine</h4>
              <h1>10(hrs)</h1>
            </div>
          </div>
          <div class="analystic">
            <div class="analystic-icon">
              <span class="bx bx-low-vision"></span>
            </div>
            <div class="analystic-info">
              <h4>Le mois</h4>
              <h1>0(hrs)</h1>
            </div>
          </div>

          <div class="analystic">
            <div class="analystic-icon">
              <span class="bx bx-low-vision"></span>
            </div>
            <div class="analystic-info">
              <h4>La année</h4>
              <h1>1450(hrs)</h1>
            </div>
          </div>
        </div>
      </section>
      <section>
        <div class="block-grid">
          <div class="revenu-card">
            <h3 class="section-head">Total</h3>
            <div class="rev-content">
              <img src="../assets/logo.png" alt="" />
              <div class="revenu-info">
                <h3>Axel Ouahmane</h3>
                <h1>35.45m <small>super</small></h1>
              </div>
              <div class="rev-sum">
                <h4>Total income</h4>
                <h2>70,859€</h2>
              </div>
            </div>
          </div>
          <div class="graph-card">
            <h3 class="section-head">Graph</h3>
            <div class="graph-content">
              <div class="graph-head">
                <div class="icon-wrapper">
                  <div class="icon">
                    <span class="bx bxs-time"></span>
                  </div>
                  <div class="icon">
                    <span class="bx bx-low-vision"></span>
                  </div>
                </div>
                <div class="graph-select">
                  <select name="" id="">
                    <option value="">September</option>
                  </select>
                </div>
              </div>
              <div class="graph-board">
                <canvas id="myChart" width="100%" height="50px"></canvas>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "DashbodrUser",
};
</script>

<style>
</style>