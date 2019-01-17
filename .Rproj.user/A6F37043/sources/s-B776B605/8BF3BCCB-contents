#' Obtuse Triangles
#' 
#' General test an obtuse triagle based on the law of cosines.
#' @param Side lengths of the triangle.
#' @export
is_obtuse <- function(x, y, z) {
  if (length(x) > 1) {
    a <- x[1]
    b <- x[2]
    c <- x[3]
  } else {
    a <- x
    b <- y
    c <- z
  }
  a^2 + b^2 < c^2 || b^2 + c^2 < a^2 || c^2 + a^2 < b^2
}


#' Generate Random Triangles
#' 
#' Generate independent random triangles centered at zero and with given radii.
#' @param n Integer specifying the number of triagles to simulate.
#' @param radii Vector giving the radii of the concentric circles.
#' @export
gen_triangles <- function(n = 1, radii = c(1, 1, 1)) {
  t(replicate(n, {
    theta <- runif(3, min = 0, max = 2*pi)
    x <- radii * cos(theta)
    y <- radii * sin(theta)
    d <- as.numeric(dist(cbind(x, y)))
    setNames(c(d, is_obtuse(d)), c("a", "b", "c", "obtuse"))
  }))
}

sim_probability <- function(radii, nsim = 1000) {
  mean(gen_triangles(n = nsim, radii)[, "obtuse"])
}


df <- expand.grid(r1 = 1:10, r2 = 1:10)
df <- df[df$r1 <= df$r2, ]
df$p <- outer(df$r1, df$r2, function(x, y) {
  mean(gen_triangles(n = 100, c(1, x, y))[, "obtuse"])
})


plot_triangle <- function(radii = c(1, 1, 1), circles = TRUE, ...) {
  theta <- runif(3, min = 0, max = 2*pi)
  X <- cbind(radii * cos(theta), radii * sin(theta))
  par(mar = c(0.1, 0.1, 0.1, 0.1))
  plot(X, type = "n", axes = FALSE, asp = 1,
       xlim = c(-max(radii), max(radii)), 
       ylim = c(-max(radii), max(radii)),
       xlab = "", ylab = "")
  if (circles) {
    plotrix::draw.circle(0, 0, radius = radii[1])
    plotrix::draw.circle(0, 0, radius = radii[2])
    plotrix::draw.circle(0, 0, radius = radii[3])
    points(0, 0, pch = 19)
    abline(v = 0, h = 0)
  }
  polygon(X, ...)
}
plot_triangle(1:3, col = adjustcolor("deepskyblue1", alpha.f = 0.5), lwd = 2)
plot_triangles <- function(n = 25, ...) {
  par(mfrow = c(n, n), mar = c(0.1, 0.1, 0.1, 0.1))
  for (i in 1:n^2) plot_triangle(...)
}

plot_triangles(radii = 1:3, col = "forestgreen", circles = TRUE)

