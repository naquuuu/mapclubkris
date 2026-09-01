# MAPCLUB Postal Code Improvement - Prototype

Clickable prototype supporting the BRD *MAPCLUB Postal Code Improvement*.

**Live:** https://naquuuu.github.io/mapclubkris/

> All names, phone numbers and street addresses in this prototype are
> fictional. The *data defects* they carry are real, reproduced from
> production records: a missing Kelurahan, a postal code written twice in
> one address line, and a `null` that leaked into a street field.

## What it shows

### Form Alamat
The web address form, in three states you can switch between.

| State | Behaviour |
|---|---|
| Sekarang | Current production form. Kode Pos is free text, validated by nothing. |
| Opsi A | Adds a Kelurahan field. Kode Pos becomes read-only and fills itself. Includes reverse lookup by postal code. |
| Opsi B | Keeps the four existing fields. Kode Pos becomes a dropdown limited to codes valid for the selected Kecamatan. |

### Alur Notifikasi
The four-layer remediation flow, in an app frame.

1. **Notifikasi** - a new `Info` tab for account-level messages
2. **Perbaiki Alamat** - fixes every flagged address in one pass
3. **Buku Alamat** - permanent badge that does not expire
4. **Checkout** - the blocking safety net

The flow carries state. Open Checkout first and it is blocked with the
shipping method greyed out. Fix the address in Perbaiki Alamat, return to
Checkout, and the block clears, RPX Regular appears, and the total updates.

The second record asks for Kecamatan *then* Kelurahan, because that address
has neither. Not every legacy record needs the same single step.

## Data

Dropdowns run on the RPX master data sample, DKI Jakarta only: 6 cities and
regencies, 44 districts, 268 sub-districts, 234 distinct postal codes. Other
provinces appear once the national file is imported.

Two structural facts from that data drive the design:

- Every Kelurahan maps to exactly **one** postal code, so the code is
  derivable and needs no customer choice.
- One postal code can cover **up to three** Kelurahan (11460 covers Jelambar,
  Jelambar Baru, Wijaya Kusuma), so reverse lookup filters the Kelurahan list
  rather than selecting it.

## Caveats

- Fonts and colours are approximated from screenshots, not lifted from
  MAPCLUB source. Reconcile with the design system before handover to Gtech.
- Static prototype. No backend, no persistence, no analytics. Refresh or
  press **Reset** to start over.

## Running it locally

Single self-contained file. Open `index.html` in a browser, or serve the
folder:

```bash
python3 -m http.server 8000
```
