# Plastic Mitra

A mobile-first React demo for connecting households, collection Mitras, recycling centres, and administrators. The interface follows the supplied Plastic Mitra mobile-app reference.

## Run locally

```sh
npm install
npm run dev
```

Open the local Vite URL. Run `npm run build` to create the production bundle.

## Android APK

The Android wrapper is generated with Capacitor. Install Android Studio with JDK 21 and Android SDK Platform/Build Tools 36, then run:

```sh
npm run android:sync
npm run android:open
```

In Android Studio, build the debug APK, or run `npm run android:apk` from Windows after setting `JAVA_HOME` and `ANDROID_SDK_ROOT`. The APK is written to `android/app/build/outputs/apk/debug/app-debug.apk`. To install over USB with Android platform tools, run `adb install -r android/app/build/outputs/apk/debug/app-debug.apk`.

To share an APK by QR code, host that file at a URL reachable from the phone (for example, on the same Wi-Fi network) and encode that download URL in the QR code.

## Demo flows

- First visit: choose a language, enter a phone number to see the OTP flow, or continue as a guest. The OTP accepts any six digits; no SMS is sent.
- Household: book a plastic pickup, follow its status, find nearby centres, and review earnings.
- Collector: open Profile and select **Collector** under **Explore demo as** to accept or complete pickups.
- Administrator: open Profile and select **Admin** to review platform activity.
- Pickup requests, the selected role, and the guest/onboarding state are saved in browser `localStorage`.

## Data model reference

The supplied ERD informs the intended server-side model. The frontend demo currently keeps sample records in local storage; it does not connect to MongoDB or implement these collections.

| Collection | Purpose and relationships |
| --- | --- |
| `users`, `addresses` | Household identities and their saved pickup addresses. |
| `collectors`, `centres` | Collection Mitra accounts and recycling-centre locations. |
| `plastic_categories` | Recyclable material types and per-unit pricing. |
| `pickup_orders`, `pickup_assignments` | A household’s pickup request and its assigned collector. |
| `collections`, `collection_items` | Completed pickups and the materials actually collected. |
| `weighing_records`, `payments` | Verified weights, calculated earnings, and payment status. |
| `buyer_accounts`, `purchase_orders`, `purchase_order_items` | Buyers and orders for sorted, traceable recycled material. |
| `inventory_batches` | Recyclables grouped for downstream processing or sale. |

Authentication, shared server persistence, live maps/geolocation, payment processing, and Vercel/Render deployment are not connected in this prototype.
