<template>
  <div id="app">
    <header>
      <div class="wrapper">
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
          <div class="container">
            <RouterLink class="navbar-brand" to="/">USIP</RouterLink>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
              data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
              aria-label="Toggle navigation">
              <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
              <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                <li class="nav-item">
                  <RouterLink class="nav-link active" to="/empleados">Empleados</RouterLink>
                </li>
                
                <li class="nav-item">
                  <RouterLink class="nav-link" to="/areas">Areas</RouterLink>
                </li>
                <li class="nav-item">
                  <RouterLink class="nav-link" to="/tipos">Tipo</RouterLink>
                </li>
                <li class="nav-item">
                  <RouterLink class="nav-link" to="/reportes">Reporte empleados</RouterLink>
                </li>
                <li class="nav-item">
                  <RouterLink class="nav-link" to="/home">Home</RouterLink>
                </li>
                <li class="nav-item">
                  <RouterLink class="nav-link" to="/about">About</RouterLink>
                </li>
                <li class="nav-item">
                  <RouterLink class="btn btn-success m-2 float-end" to="/reportes"><i class="bi bi-search"></i> Buscar
                    empleado</RouterLink>
                </li>

              </ul>
                  

            </div>
          </div>
          
        </nav>

      </div>
    </header>
    
    <div class="container mt-3">
      <router-view />
    </div>
  </div>
</template>


