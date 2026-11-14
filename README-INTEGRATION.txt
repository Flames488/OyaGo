# OyaGo role-based dashboards

## Files
- `index.html`: existing OyaGo landing page
- `ride-options.html`: passenger/driver choice after Book Ride
- `passenger-auth.html`: passenger-only sign-up/login
- `driver-auth.html`: driver-only sign-up/login
- `passenger-dashboard.html`: passenger workspace
- `driver-dashboard.html`: driver workspace
- `legal.html`: existing legal information placeholder
- `auth.html`: retained legacy page

## Dashboard navigation
Passenger: Overview, Book a ride, Ride history, Payments, My profile, Help & support.
Driver: Overview, Trip requests, Trip history, Earnings, My profile/vehicle details, Help & support.

## Authentication redirect
After a successful API response, the passenger auth page redirects to `passenger-dashboard.html` and the driver auth page redirects to `driver-dashboard.html`, unless the API returns `redirectUrl` or `requiresVerification: true`.

The auth pages expect `window.OYAGO_AUTH.registerUrl` and `window.OYAGO_AUTH.loginUrl`. Define these in a configuration script loaded before the auth page's inline script, or adapt the endpoint configuration to your existing app.

## Important production integration work
These dashboards are responsive front-end UI previews. The sample rides, names, ratings, fare and earnings are illustrative demo content, not live records. Buttons explain where service integration is needed; they do not create real rides, accept live dispatches, transfer money or persist profile changes.

Connect:
- Passenger ride request/search/cancel endpoints and live driver location/map service.
- Driver availability/heartbeat, dispatch feed, accept/decline, trip state and completion endpoints.
- Server-side authenticated session and role checks on every dashboard/API route.
- Real trip history, fares, ratings, wallet/transactions and payout APIs.
- Profile persistence, document upload and driver verification workflows.
- Payment provider, notifications, customer support and audit logging.
- Logout endpoint through `window.OYAGO_AUTH.logoutUrl` if using cookie sessions.

Do not rely on hiding dashboard links in the browser for security. Enforce authentication and passenger/driver role authorization on the server. Serve over HTTPS and use secure, HttpOnly, SameSite cookies or your application's established secure token flow.


## Local demo authentication added
When no `window.OYAGO_AUTH` endpoints are configured, sign-up and sign-in use browser localStorage/sessionStorage so the prototype can be clicked through without a backend. Passenger and driver accounts are separated by role; each role is redirected to its matching dashboard, and dashboards redirect unauthenticated or wrong-role sessions back to sign-in. This is a visual/demo convenience only: credentials are stored in browser storage and are NOT secure. Do not use this mode for real users or production. Replace it with server-side password hashing, secure HttpOnly cookies, role authorization, CSRF protection and rate limiting.

## Keke visuals and SEO
The yellow-and-black OyaGo tricycle SVG from the account chooser is reused in both role dashboards. The homepage already includes the OyaGo keke artwork. Page-specific title, meta description, keywords and social preview metadata have been added. Add the final production domain to canonical URLs and submit the sitemap/robots configuration before launch.
