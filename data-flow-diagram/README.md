# Airbnb Clone Backend - Data Flow Diagram (DFD)

This directory contains the **Data Flow Diagram (DFD)** for the Airbnb Clone backend.  
The diagram shows how data flows between users, processes, and data stores in the system.

---

## 📊 Key Elements

### External Entities
- **Guest**: Books properties, makes payments, leaves reviews.  
- **Host**: Manages property listings, responds to bookings and reviews.  
- **Admin**: Oversees users, listings, bookings, payments.  
- **Payment Gateway**: Handles secure transactions (Stripe/PayPal).  

### Processes
1. **User Management** (Registration, Login, Profile Updates)  
2. **Property Management** (Add/Edit/Delete/Search Listings)  
3. **Booking Management** (Create, Cancel, Track Bookings)  
4. **Payments** (Process guest payments, send payouts to hosts)  
5. **Reviews & Ratings** (Guests leave reviews, hosts respond)  
6. **Notifications** (Booking confirmations, cancellations, payment updates)  
7. **Admin Management** (Monitor and control system operations)  

### Data Stores
- **Users DB**  
- **Properties DB**  
- **Bookings DB**  
- **Payments DB**  
- **Reviews DB**  

---

