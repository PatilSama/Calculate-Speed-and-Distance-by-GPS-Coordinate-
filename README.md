# Calculate-Speed-and-Distance-by-GPS-Coordinate-

    public void calculateSpeedAndDist(double latitude, double longitude) {
        double newTime = System.currentTimeMillis();
//        Toast.makeText(context, "TIME = "+newTime, Toast.LENGTH_SHORT).show();
        double distance = calculationBydistance(latitude, longitude, oldLat, oldLon);
        double timeDifferent = newTime - curTime;
        speed = distance / timeDifferent;
        curTime = newTime;
        oldLat = latitude;
        oldLon = longitude;
        //  Toast.makeText(getApplication(),"SPEED 2 : "+String.valueOf(speed)+"m/s",Toast.LENGTH_SHORT).show();
    }

    public double calculationBydistance(double lat1, double lon1, double lat2, double lon2) {
        double radius = 6371000;
        double dLat = Math.toRadians(lat2 - lat1);
        double dLon = Math.toRadians(lon2 - lon1);
        double a = Math.sin(dLat / 2) * Math.sin(dLat / 2) +
                Math.cos(Math.toRadians(lat1)) * Math.cos(Math.toRadians(lat2)) *
                        Math.sin(dLon / 2) * Math.sin(dLon / 2);
        double c = 2 * Math.asin(Math.sqrt(a));
        return radius * c;
    }
    
   =====OR=======
   # Count Distance.
       private void calculateDist(double latitude, double longitude) {
        if (latitude != 0.0 && longitude != 0.0) {
            if (oldLatitude != 0.0 && oldLongitude != 0.0) {
                float[] result = new float[1];
                Location.distanceBetween(latitude, longitude, oldLatitude, oldLongitude, result);
                distmetre2 = result[0];
                double distKM = result[0] / 1000;
                totalKM += distKM;
                String total = String.valueOf(totalKM);
                totalKMS = total.substring(0, 5);
                //  Toast.makeText(this, "service KM = "+total.substring(0,5), Toast.LENGTH_SHORT).show();
            }
            oldLatitude = latitude;
            oldLongitude = longitude;
        }
    }
    
   === Get Speed ====
    private LocationCallback locationCallback = new LocationCallback() {
        @Override
        public void onLocationResult(LocationResult locationResult) {
            super.onLocationResult(locationResult);
            for (Location location : locationResult.getLocations()) {
                // Show the BusSpeed.
                busSpeedCount = (int) ((location.getSpeed() * 3600) / 1000);
            }
        }
    };
