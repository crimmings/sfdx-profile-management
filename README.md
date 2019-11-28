# SFDX PROFILE MANAGEMENT

## Problem

When pushing or pulling Profile metadata to and from a Scratch Org with Salesforce DX, the Profile file always formats to include userPermissions only. So even if your Profile metadata in your force-app file includes permissions like tabVisibility or recordTypeVisibility, the deploy/retrieve process will reset to only userPermissions.

## Solution

One way to manage this is to isolate Profile metadata outside of the force-app directory. Create a directory of Profiles and set the requisite permissions and visibilities for each Profile in the directory. To move the Profiles into your Scratch Org without reseting them to userPermissions only, use sfdx force:source:deploy **after** you use sfdx force:source:push to send the metadata in force-app to a Scratch Org. The reverse process can be used to retrieve Profile metadata from a Scratch Org. Just remember to retrieve back to your isolated Profile directory.

## Example

The force-app directory in this repository contains an example of the Admin profile as it would look after pulling Profile metadata from a Scratch Org. Notice it is all userPermissions.

The managedProfiles directory contains a sub-directory of Profiles with more specific permissions defined. By utilizing the .forceignore to ignore Profile metadata, you can avoid overwriting existing Profile metadata in source and in a Scratch Org. Rather than moving Profiles with sfdx force:source:push or sfdx force:source:pull, user sfdx force:source:retrieve or sfdx force:source:deploy to move the Profile metadata after the push or pull.

The two step process would look like this.

1. sfdx force:source:push (to default Scratch Org)
2. sfdx force:source:deploy -p managedProfiles/profiles -u defaultScratch
