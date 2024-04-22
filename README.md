# Differential Gaussian Rasterization
NOTE: this is a modified version to support feature rendering (both forward and backward) from the original repository.

**Example:**
```
others: torch.Tensor [N, S_other]
S_other = others.shape[1]

xyz_homo = torch.cat([means3D, torch.ones_like(means3D[:, :1])], dim=1)
depth = (xyz_homo @ viewpoint_camera.world_view_transform[:, 2:3])
features = torch.cat([
  others, 
  depth,
  torch.ones_like(depth),
], dim=1)

# contrib is the contributor map [1, H, W]
contrib, rendered_image, rendered_feature, radii = rasterizer(
    means3D=means3D,
    means2D=means2D,
    shs=shs,
    colors_precomp=colors_precomp,
    opacities=opacity,
    scales=scales,
    rotations=rotations,
    cov3D_precomp=cov3D_precomp,
)
rendered_other, rendered_depth, rendered_opacity = rendered_feature.split([S_other, 1, 1], dim=0)
```

Used as the rasterization engine for the paper "3D Gaussian Splatting for Real-Time Rendering of Radiance Fields". If you can make use of it in your own research, please be so kind to cite us.

<section class="section" id="BibTeX">
  <div class="container is-max-desktop content">
    <h2 class="title">BibTeX</h2>
    <pre><code>@Article{kerbl3Dgaussians,
      author       = {Kerbl, Bernhard and Kopanas, Georgios and Leimk{\"u}hler, Thomas and Drettakis, George},
      title        = {3D Gaussian Splatting for Real-Time Radiance Field Rendering},
      journal      = {ACM Transactions on Graphics},
      number       = {4},
      volume       = {42},
      month        = {July},
      year         = {2023},
      url          = {https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/}
}</code></pre>
  </div>
</section>
