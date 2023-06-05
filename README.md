import ipfs_api
import cv2

def send_photo(photo_file):
  """Sends the photo file to IPFS.

  Args:
    photo_file: The path to the photo file.

  Returns:
    The IPFS hash of the photo file.
  """
  with open(photo_file, "rb") as f:
    data = f.read()

  hash = ipfs_api.add_file(data)
  return hash

def receive_photo(hash):
  """Receives the photo file from IPFS and displays it.

  Args:
    hash: The IPFS hash of the photo file.
  """
  data = ipfs_api.get_file(hash)
  with open("photo.jpg", "wb") as f:
    f.write(data)

  # Display the photo.
  image = cv2.imread("photo.jpg")
  cv2.imshow("Photo", image)
  cv2.waitKey(0)

if __name__ == "__main__":
  # Get the path to the photo file.
  photo_file = input("Enter the path to the photo file: ")

  # Send the photo file to IPFS.
  hash = send_photo(photo_file)

  # Receive the photo file from IPFS and display it.
  receive_photo(hash)
