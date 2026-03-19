# Malibu Mod File Guide (JBeam + Required Support Files)

This repository contains a BeamNG vehicle mod for `malibu22_spadie`.

If you want to understand **what each file does** and **how everything works together**, this is the complete map.

## 1) How BeamNG assembles this mod

At a high level, BeamNG builds the vehicle like this:

1. Loads vehicle folder: `vehicles/malibu22_spadie/`
2. Reads the main vehicle definition: `malibu22_spadie.jbeam`
3. Follows `slots` from JBeam files to attach all selected parts (body, engine, suspension, wheels, lights, etc.)
4. Applies materials from `*.materials.json`
5. Loads mesh data from `malibui22_spadie.cached.dts`
6. Applies config selections from `.pc` files
7. Shows metadata/previews from `info*.json` and `*.jpg`

So:
- **JBeam files** = structure, physics, part system, slots, and many gameplay systems
- **materials files** = how meshes are shaded/textured/emissive
- **cached DTS** = actual 3D geometry data this mod references
- **PC/Info files** = user-facing configurations and metadata

---

## 2) Core files that make the vehicle exist

### `vehicles/malibu22_spadie/malibu22_spadie.jbeam`
Main/root vehicle JBeam (`slotType: main`).

What it does:
- Declares top-level slots (body, license plate design, extra mod slot)
- Defines top-level variables (example: brake force multiplier, FFB multiplier)
- Defines glowmap behavior for lights/screens/gauge indicators

This is the first JBeam anchor for the car.

### `vehicles/malibu22_spadie/malibu22_spadie_body.jbeam`
Main unibody/chassis definition.

What it does:
- Defines the unibody structure (`nodes`, `beams`, `torsionbars`, etc.)
- Exposes most major slots:
  - body panels (hood/doors/trunk/fenders/roof/bumpers)
  - glass/lights
  - engine + cooling + fuel
  - suspension + steering components
  - interior + seats + dash
  - electronics (DSE)
  - accessories (roof, tow hitch, trunk load, etc.)
- Defines camera references and some sound/soundscape settings

This is the central "hub" JBeam all major subsystems attach to.

### `vehicles/malibu22_spadie/malibui22_spadie.cached.dts`
Binary mesh file (compiled shape data).

What it does:
- Stores referenced mesh objects used by flexbodies/props
- Supplies actual renderable model geometry

Without usable mesh data, parts can still exist physically in JBeam but will not render correctly.

---

## 3) JBeam files by subsystem (what each one does)

### Powertrain / Driveline
- `malibu22_spadie_engine_i4.jbeam` - I4 engine variant (torque curve, thermals, sounds, engine slots)
- `malibu22_spadie_engine_i4_base.jbeam` - alternate/base I4 engine variant
- `malibu22_spadie_enginemounts.jbeam` - engine mounts part
- `malibu22_spadie_transaxle.jbeam` - transmission/transaxle options
- `malibu22_spadie_differential_F.jbeam` - front differential/final drive support
- `malibu22_spadie_exhaust_i4.jbeam` - exhaust section for I4
- `malibu22_spadie_muffler.jbeam` - muffler part
- `malibu22_spadie_fueltank.jbeam` - fuel tank energy storage
- `malibu22_spadie_radiator.jbeam` - radiator/cooling interface

### Brakes / Wheels / Hubs
- `malibu22_spadie_brakes.jbeam` - front/rear brake parts and slot chain
- `malibu22_spadie_hub_F.jbeam` - front hub variants
- `malibu22_spadie_hub_R.jbeam` - rear hub variants
- `malibu22_spadie_wheels.jbeam` - default wheel definitions
- `malibu22_spadie_wheels_d.jbeam` - wheel variant D
- `malibu22_spadie_wheels_ls.jbeam` - LS wheel variant
- `malibu22_spadie_wheels_lt.jbeam` - LT wheel variant
- `malibu22_spadie_wheels_rs.jbeam` - RS wheel variant

### Suspension / Steering
- `malibu22_spadie_suspension_F.jbeam` - front suspension system
- `malibu22_spadie_suspension_R.jbeam` - rear suspension system
- `malibu22_spadie_steeringwheels.jbeam` - steering wheel/interior steering part

### Electronics / Driver assists (DSE)
- `malibu22_spadie_dse.jbeam` - base Driving & Safety Electronics module
- `malibu22_spadie_dse_abs.jbeam` - ABS option module
- `malibu22_spadie_dse_esc.jbeam` - ESC option module
- `malibu22_spadie_dse_tc.jbeam` - traction control option module
- `malibu22_spadie_dse_drivemodes.jbeam` - drive mode variants/slot logic

### Body shell / Panels / Exterior structure
- `malibu22_spadie_roof.jbeam` - roof part
- `malibu22_spadie_fenders.jbeam` - fender parts
- `malibu22_spadie_hood.jbeam` - hood part
- `malibu22_spadie_trunk.jbeam` - trunk part
- `malibu22_spadie_bumper_F.jbeam` - front bumper
- `malibu22_spadie_bumper_F_a.jbeam` - front bumper alternate variant
- `malibu22_spadie_bumper_R.jbeam` - rear bumper
- `malibu22_spadie_bumperbar_F.jbeam` - front bumper support bar
- `malibu22_spadie_bumperbar_R.jbeam` - rear bumper support bar
- `malibu22_spadie_grille_F.jbeam` - front grille
- `malibu22_spadie_licenseplate.jbeam` - plate mount parts (front/rear slots)
- `malibu22_spadie_towhitch.jbeam` - tow hitch accessory
- `malibu22_spadie_roofbars.jbeam` - roof accessory/cargo bars
- `malibu22_spadie_trunk_load_cargobox.jbeam` - trunk cargo-box load part

### Doors / Glass / Mirrors / Lights
- `malibu22_spadie_doors_F.jbeam` - front doors + door-related slots
- `malibu22_spadie_doors_R.jbeam` - rear doors + door-related slots
- `malibu22_spadie_glass.jbeam` - windshield/backlight/side glass parts and break behavior
- `malibu22_spadie_mirrors.jbeam` - mirror set
- `malibu22_spadie_mirrors_a.jbeam` - alternate mirror set
- `malibu22_spadie_headlights.jbeam` - headlight assemblies
- `malibu22_spadie_taillights.jbeam` - taillight assemblies

### Interior / Occupant systems
- `malibu22_spadie_interior.jbeam` - dashboard/interior systems and slots
- `malibu22_spadie_gauges.jbeam` - gauge cluster / instrument variant
- `malibu22_spadie_airbags.jbeam` - airbags system part

---

## 4) Non-JBeam files required for the mod package to function

### Vehicle metadata and selection UI
- `info.json` - base vehicle metadata (name/brand/type/paints/default config)
- `info_1LT (A).json`
- `info_2LT (A).json`
- `info_LS (A).json`
- `info_Midnight (A).json`
- `info_Premier (A).json`
- `info_RS (A).json`
- `info_Road Trip Special (A).json`

These are per-configuration metadata entries shown in vehicle selection.

### Config presets (`.pc`)
- `1LT (A).pc`
- `2LT (A).pc`
- `LS (A).pc`
- `Midnight (A).pc`
- `Premier (A).pc`
- `RS (A).pc`
- `Road Trip Special (A).pc`

What `.pc` files do:
- Select which parts fill which slots
- Define paint values
- Set starting vehicle setup for each trim/config

### Materials
- `main.materials.json` - main Malibu materials (body/interior/light materials and map bindings)
- `screens.materials.json` - digital screen/gauge screen materials

### Borrowed/vanilla material bundles
Folder: `vinillia_materials_main/`
- `bastion.materials.json`
- `lansdale.materials.json`
- `legarn.materials.json`
- `midsize.materials.json`
- `roamer.materials.json`
- `sunburst2.materials.json`
- `vivace.materials.json`

These provide additional material definitions referenced by parts, gauges, decals, or reused meshes.

### Thumbnails / images
- `default.jpg`
- `1LT (A).jpg`
- `2LT (A).jpg`
- `LS (A).jpg`
- `Midnight (A).jpg`
- `Premier (A).jpg`
- `RS (A).jpg`
- `Road Trip Special (A).jpg`

Used by the BeamNG vehicle/config selection UI.

### Texture assets present in folder
Examples:
- `malibu22_spadie_screens.dds`
- `malibu22_spadie_glass_dmg_*.png/.DDS/.dds`

These support material maps, screen appearance, and glass damage visuals.

---

## 5) How files depend on each other (practical chain)

Typical dependency chain for one loaded configuration:

1. `*.pc` selects top-level `mainPartName` and part slot fills
2. `malibu22_spadie.jbeam` loads root slots
3. `malibu22_spadie_body.jbeam` loads core structure and most subsystem slots
4. Subsystem JBeams (engine/suspension/wheels/lights/interior/etc.) load according to chosen slot options
5. Flexbodies in JBeams reference mesh names from `malibui22_spadie.cached.dts`
6. Material names from flexbodies/glowmaps resolve via `main.materials.json`, `screens.materials.json`, and `vinillia_materials_main/*.materials.json`
7. `info*.json` + `*.jpg` present the config in UI

If any required link is missing (slot part, mesh name, material name), you usually get missing parts, invisible meshes, or pink/no-material surfaces.

---

## 6) Editing guidance (safe workflow)

- Change **slot structure** in JBeam first (root/body and subsystem slots)
- Keep part names and slot types consistent between:
  - JBeam part names
  - `.pc` selected parts
  - material map names (`mapTo`)
  - mesh names in flexbodies
- After renaming materials/meshes, verify all references across JBeam + materials files
- Keep config files (`.pc` + `info_*.json`) aligned so trims appear correctly in UI

---

## 7) Quick troubleshooting map

- Missing part in parts menu/loadout: usually slot mismatch (`slotType` vs selected part)
- Car loads but major section invisible: missing/bad mesh reference in flexbodies or missing cached model data
- Pink/unstyled surfaces: material name mismatch or missing texture map
- Config appears but wrong parts spawn: `.pc` points to wrong part keys or old names

---

If you want, next step can be a second document that traces **exact slot trees** (root -> body -> subsystem -> subpart) for each trim (`1LT`, `2LT`, `RS`, etc.).
