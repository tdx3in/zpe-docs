---
title: ZPE Systems
---

{{< blocks/cover title="Welcome to ZPE Systems Product Documentation!" image_anchor="top" height="half" >}}

Set up, configure, or manage your product. Access all information in one single platform.
{{< /blocks/cover >}}

<style>
/* Desktop: Default styling for the tiles */
.tiles-container {
  display: flex;
  justify-content: space-around;
  gap: 20px;
  padding: 20px;
}

.tile {
  width: 250px;
  height: 150px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  color: #333;
  transition: transform 0.3s, box-shadow 0.3s;
  text-decoration: none;
}

.tile:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  transform: translateY(-5px);
}

.tile-icon {
  font-size: 40px;
  margin-bottom: 10px;
}

/* Tablet: Stack tiles vertically */
@media (max-width: 768px) {
  .tiles-container {
    flex-direction: column;
    align-items: center;
  }
}

/* Mobile: Adjust tile width and padding */
@media (max-width: 480px) {
  .tile {
    width: 90%; /* Adjust width to fit smaller screens */
    height: auto;
    padding: 20px;
  }

  .tiles-container {
    padding: 10px;
  }
}
</style>

<div class="tiles-container">
  <a href="/new-docs/docs/" class="tile">
    <i class="fas fa-cogs tile-icon" style="color: #007BFF;"></i>
    <h4>Nodegrid OS</h4>
    <p>Explore all the powerful features of ZPE Systems products.</p>
  </a>

  <a href="/new-docs/docs/" class="tile">
    <i class="fas fa-book tile-icon" style="color: #28a745;"></i>
    <h4>ZPE Cloud</h4>
    <p>Access detailed documentation, guides, and resources.</p>
  </a>

  <a href="/new-docs/docs/" class="tile">
    <i class="fas fa-users tile-icon" style="color: #dc3545;"></i>
    <h4>Reference Guides</h4>
    <p>Join discussions and collaborate with our vibrant community.</p>
  </a>
</div>
