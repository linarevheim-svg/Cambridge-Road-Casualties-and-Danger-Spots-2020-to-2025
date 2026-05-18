# ── Cambridgeshire Road Casualties — Data Filtering Script ───────────
# Run in Google Colab after uploading the two STATS19 CSV files
# Downloads: https://www.gov.uk/government/statistical-data-sets/road-safety-open-data

import pandas as pd

# ── 1. Load the national collisions file ─────────────────────────────
# Upload dft-road-casualty-statistics-collision-last-5-years.csv to Colab first

print("Loading collisions file... (this may take 30-60 seconds)")
collisions = pd.read_csv("dft-road-casualty-statistics-collision-last-5-years.csv",
                         low_memory=False)

print(f"Total GB collisions loaded: {len(collisions):,}")
print("Columns:", collisions.columns.tolist())

# ── 2. Check local authority codes ───────────────────────────────────
# Preview unique local authority district values
print("\nSample local authority values:")
print(collisions["local_authority_district"].value_counts().head(20))

# ── 3. Filter to Cambridgeshire ──────────────────────────────────────
# Local authority district codes for Cambridgeshire:
# 114 = Cambridge City
# 115 = East Cambridgeshire
# 116 = Fenland
# 117 = Huntingdonshire
# 118 = South Cambridgeshire
# 113 = Peterborough (unitary)

cambs_codes = [113, 114, 115, 116, 117, 118]

cambs_collisions = collisions[
    collisions["local_authority_district"].isin(cambs_codes)
].copy()

print(f"\nCambridgeshire collisions: {len(cambs_collisions):,}")
print(f"Years present: {sorted(cambs_collisions['accident_year'].unique())}")
print(f"\nBy local authority:")
print(cambs_collisions["local_authority_district"].value_counts())

# ── 4. Save filtered collisions ───────────────────────────────────────
cambs_collisions.to_csv("collisions_cambridgeshire.csv", index=False)
print("\n✓ Saved collisions_cambridgeshire.csv")

# ── 5. Load and filter casualties file ───────────────────────────────
print("\nLoading casualties file...")
casualties = pd.read_csv("dft-road-casualty-statistics-casualty-last-5-years.csv",
                         low_memory=False)

print(f"Total GB casualties loaded: {len(casualties):,}")

# Join casualties to Cambridgeshire collisions using accident_index
cambs_accident_ids = set(cambs_collisions["accident_index"])
cambs_casualties = casualties[
    casualties["accident_index"].isin(cambs_accident_ids)
].copy()

print(f"Cambridgeshire casualties: {len(cambs_casualties):,}")
print(f"\nCasualty types:")
print(cambs_casualties["casualty_type"].value_counts())

# ── 6. Save filtered casualties ───────────────────────────────────────
cambs_casualties.to_csv("casualties_cambridgeshire.csv", index=False)
print("\n✓ Saved casualties_cambridgeshire.csv")

# ── 7. Quick summary stats ────────────────────────────────────────────
print("\n── SUMMARY ──────────────────────────────────────────")
print(f"Total collisions in Cambridgeshire 2020-2024: {len(cambs_collisions):,}")
print(f"Total casualties in Cambridgeshire 2020-2024: {len(cambs_casualties):,}")
print(f"\nSeverity breakdown (collisions):")

print(cambs_collisions["accident_severity"].value_counts())
print(f"\nYear breakdown:")
print(cambs_collisions["accident_year"].value_counts().sort_index())
