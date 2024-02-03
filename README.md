from mpl_toolkits.mplot3d import Axes3D
from skimage import measure
from matplotlib import cm
n = 100
x = np.linspace(-3,3,n)
y = np.linspace(-3,3,n)
z = np.linspace(-3,3,n)
X, Y, Z =  np.meshgrid(x, y, z)
def f_heart(x,y,z):
    F = 320 * ((-x**2 * z**3 -9*y**2 * z**3/80) + (x**2 + 9*y**2/4 + z**2-1)**3)
    return F
vol = f_heart(X,Y,Z) 
verts, faces ,_ ,_ = measure.marching_cubes_lewiner(vol, 0, spacing=(0.1, 0.1, 0.1))
fig = plt.figure(figsize=(12,8))
ax = fig.add_subplot(111, projection='3d')
ax.plot_trisurf(verts[:, 0], verts[:,1], faces, verts[:, 2],cmap=cm.Reds,edgecolor='white')
ax.view_init(15, -15)
ax.grid(False)
plt.axis('off')
plt.show()
