pg_dump --data-only --dbname=stats_dev > stats_dev_data.sql




pg_dump \
  --data-only \
  --inserts \
  --exclude-schema=pgpm_migrate \
  stats_dev > stats_dev_inserts.sql


<= PG 16

pg_dump \
  --data-only \
  --inserts \
  --no-owner \
  --no-privileges \
  --no-comments \
  --no-tablespaces \
  --no-security-labels \
  --exclude-schema=pgpm_migrate \
  stats_dev \
  | sed '/^SET /d' | sed '/^SELECT pg_catalog.set_config/d' \
  > stats_dev_inserts.sql

> PG 16

pg_dump \
  --data-only \
  --inserts \
  --no-owner \
  --no-privileges \
  --exclude-schema=pgpm_migrate \
  --no-set-output \
  stats_dev > stats_dev_inserts.sql

