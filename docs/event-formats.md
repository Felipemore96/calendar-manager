# Event formats

Titles and descriptions are in Spanish. Dates in descriptions use `DD-MM-YYYY`. Leave out a line when the email doesn't give that detail. Every description ends with the `[calendar-agent]` marker line (see `CLAUDE.md`, step 5).

Placeholders are in `<angle brackets>`.

## flight ✈️

- **Title:** `✈️ Vuelo <flightNo> <FROM> → <TO>`, using IATA airport codes.
- **Timing:** departure to arrival, each in the local timezone of its airport.
- **Location:** `<departure airport name> (<FROM>)`
- **Description:**
  ```
  Aerolínea: <airline>
  Reserva: <PNR>
  Salida: <terminal / gate if given>
  Llegada: <terminal if given>
  Asiento: <seat>
  Pasajeros: <names>
  Email: <gmail link>
  [calendar-agent] gmail:<threadId> ref:<PNR>
  ```
- One event per leg. A layover means two events.

Example: `✈️ Vuelo KL1701 AMS → MAD`, 14:05 to 16:40.

## train 🚆 / bus 🚌

- **Title:** `🚆 Tren <from> → <to>` or `🚌 Bus <from> → <to>`
- **Timing:** departure to arrival.
- **Location:** departure station.
- **Description:** operator, booking reference, coach and seat, Gmail link, marker.

## car_rental 🚗

- **Title:** `🚗 Alquiler coche: <company>`
- **Timing:** pickup to return time, as one event. If it spans more than 2 days, create an all-day event from the pickup date to the return date instead, with the times in the description.
- **Location:** pickup location.
- **Description:** company, reference, pickup and return location and time, car category, Gmail link, marker.

## stay 🏨

- **Title:** `🏨 Alojamiento: <property name>`
- **Timing:** all-day, covering the check-in day through the check-out day. Google Calendar's all-day end date is exclusive, so set **start = check-in date** and **end = check-out date + 1 day**.
- **Location:** property address.
- **Description:**
  ```
  Check-in: <DD-MM-YYYY HH:MM>
  Check-out: <DD-MM-YYYY HH:MM>
  Reserva: <ref> (<platform>)
  Dirección: <address>
  Huéspedes: <n>
  Contacto: <host phone if given>
  Email: <gmail link>
  [calendar-agent] gmail:<threadId> ref:<ref>
  ```

## reservation 🍽️

- **Title:** `🍽️ Reserva: <restaurant>`
- **Timing:** the booked time. Default duration is 2 h if no end is given.
- **Location:** restaurant address.
- **Description:** number of people, name on the booking, reference, Gmail link, marker.

## ticket 🎟️

- **Title:** `🎟️ <event name>`
- **Timing:** start time. Use the end time if given, otherwise a default of 2 h 30 min. If only the doors-open time is given, use it and say so in the description.
- **Location:** venue.
- **Description:** venue, number of tickets, seats or section, reference, Gmail link, marker.

## appointment 🩺

- **Title:** `🩺 Cita: <what / with whom>`, for example `🩺 Cita: dentista`. Use a fitting emoji for clearly non-medical appointments: `💇 Cita: peluquería`, `🏠 Visita: <address>`, `🏛️ Cita: <office>`.
- **Timing:** the booked time. Default duration is 1 h if no end is given.
- **Location:** address.
- **Description:** practitioner or office, for whom, what to bring if stated, reference, Gmail link, marker.

## delivery 📦

- **Title:** `📦 Entrega: <shop>, <item>`. Keep `<item>` short, for example `📦 Entrega: Coolblue, lavadora`. With many items, use `pedido <orderNo>`.
- **Timing:**
  - with a time window: a timed event over that window.
  - with only a date: all-day on that date.
  - with a date range ("between Tue and Thu"): all-day on the first date, with `Por revisar: rango <DD-MM> a <DD-MM>` in the description and the `❓` prefix.
- **Location:** none.
- **Description:** carrier, tracking number, order number, Gmail link, marker.
- When a tracking update moves the date, update the existing event (step 6, change).

## Uncertain events ❓

Prefix the title with `❓ ` and start the description with `Por revisar: <what is unclear>`. Example:

```
❓ 🩺 Cita: fisioterapia
Por revisar: el email no indica AM/PM; se asume 10:00.
...
```
