(cosmology)=
# Cosmology

The `/Cosmology` group contains information on the cosmological parameters used in the simulation. 
The `Is_cosmological` attribute is **required**. 
Other fields may be required (see [](#cosmo-is_cosmological)) and all other fields are considered "best-effort".

## Attributes

We don't include a types column as all fields are `number`s, unless otherwise marked.
Likewise the default value is  `-1` unless specified.

| Name                   | Required if cosmological | Link                              |
| ---------------------- | :----------------------: | --------------------------------- |
| Is_cosmological[^bool] |           N/A            | [](#cosmo-is_cosmological)        |
| Omega_matter           |            X             | [](#cosmo-omega_matter)           |
| Omega_lambda           |            X             | [](#cosmo-omega_lambda)           |
| h                      |            X             | [](#cosmo-littleH)                |
| Redshift               |            X             | [](#cosmo-redshift)               |
| Scale-factor           |            X             | [](#cosmo-scale-factor)           |
| H                      |                          | [](#cosmo-bigH)                   |
| H0                     |                          | [](#cosmo-H0)                     |
| Critical_density       |                          | [](#cosmo-critical_density)       |
| Critical_density_at_z0 |                          | [](#cosmo-critical_density_at_z0) |
| Hubble_time            |                          | [](#cosmo-hubble_time)            |
| Lookback_time          |                          | [](#cosmo-lookback_time)          |
| Mean_baryon_density    |                          | [](#cosmo-mean_baryon_density)    |
| Mean_matter_density    |                          | [](#cosmo-mean_matter_density)    |
| N_eff                  |                          | [](#cosmo-n_eff)                  |
| Omega_baryon           |                          | [](#cosmo-omega_baryon)           |
| Omega_darkmatter       |                          | [](#cosmo-omega_darkmatter)       |
| Omega_radiation        |                          | [](#cosmo-omega_radiation)        |
| Omega_curvature        |                          | [](#cosmo-omega_curvature)        |
| T_CMB_0_SI             |                          | [](#cosmo-t_cmb_0_si)             |
| T_CMB_0                |                          | [](#cosmo-t_cmb_0)                |
| Universe_age           |                          | [](#cosmo-universe_age)           |
| a_begin                |                          | [](#cosmo-a_begin)                |
| a_end                  |                          | [](#cosmo-a_end)                  |
| time_begin             |                          | [](#cosmo-time_begin)             |
| time_end               |                          | [](#cosmo-time_end)               |
| w                      |                          | [](#cosmo-w)                      |
| w_0                    |                          | [](#cosmo-w_0)                    |
| w_a                    |                          | [](#cosmo-w_a)                    |

[^bool]: This field can be a boolean, instead of an integer/floating point number.

(cosmo-is_cosmological)=
### `Is_cosmological`

Flag for whether this snapshot represents a cosmological simulation. Default is `0/False`.  
If it is cosmological, the marked fields are also considered to be required. 
If false, the marked fields can use the provided default values, however we recommend using the actual values, if possible.

(cosmo-omega_matter)=
### `Omega_matter`

Matter density ($\Omega_M$, not $\Omega_{M}h^2$) at $z=0$ in units of the critical density.


(cosmo-omega_lambda)=
### `Omega_lambda`

Vacuum energy density ($\Omega_{\Lambda}$) at $z=0$ in units of the critical density.

(cosmo-littleH)=
### `h`

Gives $h$, the Hubble Constant in units of $100 \text{ km}\text{s}^{-1}\text{Mpc}^{-1}$, thus $H_0=100h$ (see [](#cosmo-H0)).

(cosmo-redshift)=       
### `Redshift`

The cosmological redshift ($z$) of this snapshot. Defaults to -1.  Only well-defined if simulation is cosmological and/or [`/Header.Time`](#header-time)=0. Should be identical to [`/Header.Redshift`](#header-redshift), if present. See also [](#cosmo-scale-factor).

(cosmo-scale-factor)=          
### `Scale-factor`

The cosmological scale-factor of this snapshot, defined $a=\frac{a_0}{(1+z)}$. Only well-defined if simulation is cosmological and/or [`/Header.Time`](#header-time)=0. See also [](#cosmo-redshift).

(cosmo-bigH)=
### `H`

Gives $H$, the Hubble Parameter, as defined in the (1st) Friedmann equation: $H^2=\frac{8\pi G}{3}\rho(t)-\frac{\kappa c^2}{a^2(t)}+\frac{\Lambda c^2}{3}$, where $\rho(t)$ is the universe's energy density, $\kappa$ is the scalar curvature parameter (see [](#cosmo-omega_curvature)), $a(t)$ is the [](#cosmo-scale-factor), and $\Lambda$ is the cosmological constant (see [](#cosmo-omega_lambda)).

(cosmo-H0)=
### `H0`

Gives $H_0$, the Hubble Constant in units of $\text{ km}\text{s}^{-1}\text{Mpc}^{-1}$, so $H_0=100 h$. (see [](#cosmo-littleh)).

(cosmo-critical_density)=
### `Critical_density`

Critical density of the universe at this snapshot, $\rho_c=\frac{3 H^2}{8\pi G}$ assuming a flat universe and $\Lambda=0$.


(cosmo-critical_density_at_z0)=
### `Critical_density_at_z0`

Critical density of the universe at the redshift $z=0$: $\rho_{c,0}=\frac{3H_0^2}{8\pi G}$.


(cosmo-hubble_time)=
### `Hubble_time`

Inverse of the Hubble constant, [$H_0$](#cosmo-H0) in Internal Units.

(cosmo-lookback_time)=
### `Lookback_time`

Lookback time of the this snapshot in Internal Units.


(cosmo-mean_baryon_density)=
### `Mean_baryon_density`

Mean baryon density in Internal Units.


(cosmo-mean_matter_density)=
### `Mean_matter_density`

Mean matter density in Internal Units.

(cosmo-n_eff)=
### `N_eff`

The effective number of neutrinos.

(cosmo-omega_baryon)=              
### `Omega_baryon`

Baryonic matter density ($\Omega_b$, not $\Omega_{b}h^2$) at $z=0$ in units of the critical density. 
Note that $\Omega_M=\Omega_b + \Omega_{DM}$.

(cosmo-omega_darkmatter)=
### `Omega_darkmatter`

Dark matter density ($\Omega_{DM}$, not $\Omega_{DM}h^2$) at $z=0$ in units of the critical density. 
Note that $\Omega_M=\Omega_b + \Omega_{DM}$


(cosmo-omega_radiation)=    
### `Omega_radiation`

Relativistic/radiation density ($\Omega_{r}\equiv\Omega_{\gamma}$, not $\Omega_{r}h^2$) at $z=0$ in units of the critical density.

(cosmo-omega_curvature)=        
### `Omega_curvature`

Curvature "density" ($\Omega_k$, not $\Omega_{k}h^2$) at $z=0$ in units of the critical density.
Note: $\Omega_k=1-(\Omega_M+\Omega_{r}+\Omega_{\Lambda})$

(cosmo-t_cmb_0_si)=
### `T_CMB_0_SI`

Temperature of the Cosmic Microwave Background at $z=0$ in Kelvin.


(cosmo-t_cmb_0)=
### `T_CMB_0`

Temperature of the Cosmic Microwave Background at $z=0$ in Internal Units.


(cosmo-universe_age)=       
### `Universe_age`

Age of the universe at this snapshot in Internal Units.


(cosmo-a_begin)=
### `a_begin`

Initial scale-factor for the simulation.

(cosmo-a_end)=          
### `a_end`

Final scale-factor for the simulation.

(cosmo-time_begin)=            
### `time_begin`

Initial time of the simulation in Internal Units.

(cosmo-time_end)=
### `time_end`

Final time of the simulation in Internal Units.

(cosmo-w)=         
### `w`

Dark energy equation of state at this snapshot, defined as $w(a)=w_0 + w_a(1-a)$, where $w_0$ is [](#cosmo-w_0), $a$ is the [](#cosmo-scale-factor), and $w_a$ is [](#cosmo-w_a).


(cosmo-w_0)=              
### `w_0`

The $z=0$ dark energy equation of state parameter, $w_0$.
See [](#cosmo-w)

(cosmo-w_a)=              
### `w_a`

The dark energy equation of state evolution parameter, $w_a$.
See [](#cosmo-w)
