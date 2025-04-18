{
  "openapi": "3.0.0",
  "info": {
    "title": "API Documentation",
    "version": "1.0.0",
    "description": "This is the API documentation for the site, powered by Mash Server."
  },
  "paths": {
    "/api/api-key/{id}": {
      "del": {
        "summary": "Deletes an API key",
        "description": "Deletes an API key by its ID.",
        "operationId": "deleteApiKey",
        "tags": [
          "API Key Management"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The ID of the API key to delete",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "API key deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized"
          },
          "404": {
            "description": "API key not found"
          },
          "500": {
            "description": "Server error"
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "put": {
        "summary": "Updates an API key",
        "description": "Updates an API key's details such as permissions, IP whitelist, or IP restriction.",
        "operationId": "updateApiKey",
        "tags": [
          "API Key Management"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The ID of the API key to update",
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "description": "Data for updating the API key",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "permissions": {
                    "type": "array",
                    "items": {
                      "type": "string"
                    },
                    "description": "Updated permissions associated with the API key"
                  },
                  "ipWhitelist": {
                    "type": "array",
                    "items": {
                      "type": "string"
                    },
                    "description": "Updated IP whitelist for the API key"
                  },
                  "ipRestriction": {
                    "type": "boolean",
                    "description": "Updated IP restriction setting (true for restricted, false for unrestricted)"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "API key updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string"
                    },
                    "permissions": {
                      "type": "array",
                      "items": {
                        "type": "string"
                      }
                    },
                    "ipWhitelist": {
                      "type": "array",
                      "items": {
                        "type": "string"
                      }
                    },
                    "ipRestriction": {
                      "type": "boolean"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized"
          },
          "404": {
            "description": "API key not found"
          },
          "500": {
            "description": "Server error"
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/api-key": {
      "get": {
        "summary": "Lists all API keys",
        "description": "Retrieves all API keys associated with the authenticated user.",
        "operationId": "listApiKeys",
        "tags": [
          "API Key Management"
        ],
        "responses": {
          "200": {
            "description": "API keys retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string"
                      },
                      "name": {
                        "type": "string"
                      },
                      "key": {
                        "type": "string"
                      },
                      "permissions": {
                        "type": "array",
                        "items": {
                          "type": "string"
                        }
                      },
                      "ipWhitelist": {
                        "type": "array",
                        "items": {
                          "type": "string"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized"
          },
          "500": {
            "description": "Server error"
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Creates a new API key",
        "description": "Generates a new API key for the authenticated user.",
        "operationId": "createApiKey",
        "tags": [
          "API Key Management"
        ],
        "requestBody": {
          "description": "Data required to create a new API key",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "name": {
                    "type": "string",
                    "description": "Name of the API key"
                  },
                  "permissions": {
                    "type": "array",
                    "items": {
                      "type": "string"
                    },
                    "description": "Permissions associated with the API key"
                  },
                  "ipWhitelist": {
                    "type": "array",
                    "items": {
                      "type": "string"
                    },
                    "description": "IP addresses whitelisted for the API key"
                  },
                  "ipRestriction": {
                    "type": "boolean",
                    "description": "Restrict access to specific IPs (true) or allow unrestricted access (false)"
                  }
                },
                "required": [
                  "name"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "API key created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string"
                    },
                    "name": {
                      "type": "string"
                    },
                    "key": {
                      "type": "string"
                    },
                    "permissions": {
                      "type": "array",
                      "items": {
                        "type": "string"
                      }
                    },
                    "ipWhitelist": {
                      "type": "array",
                      "items": {
                        "type": "string"
                      }
                    },
                    "ipRestriction": {
                      "type": "boolean"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "API key limit reached"
          },
          "401": {
            "description": "Unauthorized"
          },
          "500": {
            "description": "Server error"
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/delete/confirm": {
      "post": {
        "summary": "Check account deletion code and delete user",
        "operationId": "checkAccountDeletionCode",
        "tags": [
          "Account"
        ],
        "description": "Checks the deletion code, deletes the user's account if valid, and sends a confirmation email.",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user confirming account deletion"
                  },
                  "token": {
                    "type": "string",
                    "description": "Account deletion confirmation token"
                  }
                },
                "required": [
                  "email",
                  "token"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User account deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request or token",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/auth/delete": {
      "post": {
        "summary": "Generate account deletion confirmation code",
        "operationId": "generateAccountDeletionCode",
        "tags": [
          "Account"
        ],
        "description": "Generates a code for confirming account deletion and sends it to the user's email.",
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user requesting account deletion"
                  }
                },
                "required": [
                  "email"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Deletion confirmation code generated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/login/chat": {
      "get": {
        "summary": "Logs in a user to the chat service",
        "description": "Logs in a user to the chat service and returns a session token",
        "operationId": "loginUserChat",
        "tags": [
          "Auth"
        ],
        "requiresAuth": false,
        "parameters": [
          {
            "in": "query",
            "name": "email",
            "required": true,
            "schema": {
              "type": "string",
              "format": "email"
            },
            "description": "Email of the user"
          },
          {
            "in": "query",
            "name": "password",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "Password of the user"
          },
          {
            "in": "query",
            "name": "firstName",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "First name of the user"
          },
          {
            "in": "query",
            "name": "lastName",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "Last name of the user"
          }
        ],
        "responses": {
          "200": {
            "description": "User logged into chat successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "cookies": {
                      "type": "object",
                      "properties": {
                        "accessToken": {
                          "type": "string",
                          "description": "Access token"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing or invalid email/password)"
          },
          "401": {
            "description": "Unauthorized (incorrect credentials)"
          }
        },
        "security": []
      }
    },
    "/api/auth/login/flutter": {
      "post": {
        "summary": "Logs in a user",
        "description": "Logs in a user and returns a session token",
        "operationId": "loginUser",
        "tags": [
          "Auth"
        ],
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user"
                  },
                  "password": {
                    "type": "string",
                    "description": "Password of the user"
                  }
                },
                "required": [
                  "email",
                  "password"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User logged in successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "twoFactor": {
                      "type": "object",
                      "properties": {
                        "enabled": {
                          "type": "boolean",
                          "description": "2FA enabled status"
                        },
                        "type": {
                          "type": "string",
                          "description": "Type of 2FA"
                        }
                      }
                    },
                    "id": {
                      "type": "string",
                      "description": "User ID"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., invalid email or password)"
          },
          "401": {
            "description": "Unauthorized (e.g., incorrect email or password)"
          }
        },
        "security": []
      }
    },
    "/api/auth/login/google": {
      "post": {
        "summary": "Logs in a user with Google",
        "operationId": "loginUserWithGoogle",
        "tags": [
          "Auth"
        ],
        "description": "Logs in a user using Google and returns a session token",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "token": {
                    "type": "string",
                    "description": "Google OAuth token"
                  },
                  "ref": {
                    "type": "string",
                    "description": "Referral code"
                  }
                },
                "required": [
                  "token"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User logged in successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "cookies": {
                      "type": "object",
                      "properties": {
                        "accessToken": {
                          "type": "string",
                          "description": "Access token"
                        },
                        "sessionId": {
                          "type": "string",
                          "description": "Session ID"
                        },
                        "csrfToken": {
                          "type": "string",
                          "description": "CSRF token"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/auth/login": {
      "post": {
        "summary": "Logs in a user",
        "description": "Logs in a user and returns a session token",
        "operationId": "loginUser",
        "tags": [
          "Auth"
        ],
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user"
                  },
                  "password": {
                    "type": "string",
                    "description": "Password of the user"
                  },
                  "recaptchaToken": {
                    "type": "string",
                    "description": "Recaptcha token if enabled",
                    "nullable": true
                  }
                },
                "required": [
                  "email",
                  "password"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User logged in successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "twoFactor": {
                      "type": "object",
                      "properties": {
                        "enabled": {
                          "type": "boolean",
                          "description": "2FA enabled status"
                        },
                        "type": {
                          "type": "string",
                          "description": "Type of 2FA"
                        }
                      }
                    },
                    "id": {
                      "type": "string",
                      "description": "User ID"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., invalid email or password)"
          },
          "401": {
            "description": "Unauthorized (e.g., incorrect email or password)"
          }
        },
        "security": []
      }
    },
    "/api/auth/login/nonce": {
      "get": {
        "summary": "Generates a nonce for client use",
        "operationId": "generateNonce",
        "tags": [
          "Auth"
        ],
        "description": "Generates a nonce for client use",
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Nonce generated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "nonce": {
                      "type": "string",
                      "description": "The generated nonce"
                    }
                  },
                  "required": [
                    "nonce"
                  ]
                }
              }
            }
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": []
      }
    },
    "/api/auth/login/wallet": {
      "post": {
        "summary": "Logs in a user with SIWE",
        "description": "Logs in a user using Sign-In With Ethereum (SIWE)",
        "operationId": "siweLogin",
        "tags": [
          "Auth"
        ],
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "message": {
                    "type": "string",
                    "description": "SIWE message"
                  },
                  "signature": {
                    "type": "string",
                    "description": "Signature of the SIWE message"
                  }
                },
                "required": [
                  "message",
                  "signature"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User logged in successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "id": {
                      "type": "string",
                      "description": "User ID"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., invalid message or signature)"
          },
          "401": {
            "description": "Unauthorized (e.g., signature verification failed)"
          }
        },
        "security": []
      }
    },
    "/api/auth/logout": {
      "post": {
        "summary": "Logs out the current user",
        "operationId": "logoutUser",
        "tags": [
          "Auth"
        ],
        "description": "Logs out the current user and clears all session tokens",
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "User logged out successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, no user to log out"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/otp/generate": {
      "post": {
        "summary": "Generates an OTP secret",
        "operationId": "generateOTPSecret",
        "tags": [
          "Auth"
        ],
        "description": "Generates an OTP secret for the user",
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "type": {
                    "type": "string",
                    "enum": [
                      "EMAIL",
                      "SMS",
                      "APP"
                    ],
                    "description": "Type of 2FA"
                  },
                  "phoneNumber": {
                    "type": "string",
                    "description": "Phone number for SMS OTP"
                  }
                },
                "required": [
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP secret generated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "secret": {
                      "type": "string",
                      "description": "Generated OTP secret"
                    },
                    "qrCode": {
                      "type": "string",
                      "description": "QR code for APP OTP"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request"
          },
          "401": {
            "description": "Unauthorized"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/otp/login": {
      "post": {
        "summary": "Verifies the OTP for login",
        "operationId": "verifyLoginOTP",
        "tags": [
          "Auth"
        ],
        "description": "Verifies the OTP for login and returns a session token",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "id": {
                    "type": "string",
                    "format": "uuid",
                    "description": "ID of the user"
                  },
                  "otp": {
                    "type": "string",
                    "description": "OTP to verify"
                  }
                },
                "required": [
                  "id",
                  "otp"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP verified successfully, user logged in",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing parameters, invalid OTP)"
          },
          "401": {
            "description": "Unauthorized (incorrect or expired OTP)"
          }
        },
        "security": []
      }
    },
    "/api/auth/otp/resend": {
      "post": {
        "summary": "Resends the OTP for 2FA",
        "operationId": "resendOtp",
        "tags": [
          "Auth"
        ],
        "description": "Resends the OTP for 2FA",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "id": {
                    "type": "string",
                    "format": "uuid",
                    "description": "ID of the user"
                  },
                  "type": {
                    "type": "string",
                    "enum": [
                      "EMAIL",
                      "SMS"
                    ],
                    "description": "Type of 2FA"
                  }
                },
                "required": [
                  "id",
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP resent successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request"
          },
          "401": {
            "description": "Unauthorized"
          }
        },
        "security": []
      }
    },
    "/api/auth/otp/save": {
      "post": {
        "summary": "Saves the OTP",
        "operationId": "saveOTP",
        "tags": [
          "Auth"
        ],
        "description": "Saves the OTP secret and type for the user",
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "secret": {
                    "type": "string",
                    "description": "Generated OTP secret"
                  },
                  "type": {
                    "type": "string",
                    "enum": [
                      "EMAIL",
                      "SMS",
                      "APP"
                    ],
                    "description": "Type of 2FA"
                  }
                },
                "required": [
                  "secret",
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP saved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request"
          },
          "401": {
            "description": "Unauthorized"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/otp/toggle": {
      "post": {
        "summary": "Toggles OTP status",
        "operationId": "toggleOtp",
        "tags": [
          "Auth"
        ],
        "description": "Enables or disables OTP for the user",
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "status": {
                    "type": "boolean",
                    "description": "Status to set for OTP (enabled or disabled)"
                  }
                },
                "required": [
                  "status"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP status updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request"
          },
          "401": {
            "description": "Unauthorized"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/otp/verify": {
      "post": {
        "summary": "Verifies the OTP",
        "operationId": "verifyOTP",
        "tags": [
          "Auth"
        ],
        "description": "Verifies the OTP and saves it",
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "otp": {
                    "type": "string",
                    "description": "OTP to verify"
                  },
                  "secret": {
                    "type": "string",
                    "description": "Generated OTP secret"
                  },
                  "type": {
                    "type": "string",
                    "enum": [
                      "EMAIL",
                      "SMS",
                      "APP"
                    ],
                    "description": "Type of 2FA"
                  }
                },
                "required": [
                  "otp",
                  "secret",
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP verified and saved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request"
          },
          "401": {
            "description": "Unauthorized"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/register/google": {
      "post": {
        "summary": "Registers a new user with Google",
        "operationId": "registerUserWithGoogle",
        "tags": [
          "Auth"
        ],
        "description": "Registers a new user using Google and returns a session token",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "token": {
                    "type": "string",
                    "description": "Google OAuth token"
                  },
                  "ref": {
                    "type": "string",
                    "description": "Referral code"
                  }
                },
                "required": [
                  "token"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User registered successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "cookies": {
                      "type": "object",
                      "properties": {
                        "accessToken": {
                          "type": "string",
                          "description": "Access token"
                        },
                        "sessionId": {
                          "type": "string",
                          "description": "Session ID"
                        },
                        "csrfToken": {
                          "type": "string",
                          "description": "CSRF token"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/auth/register": {
      "post": {
        "summary": "Registers a new user",
        "operationId": "registerUser",
        "tags": [
          "Auth"
        ],
        "description": "Registers a new user and returns a session token",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "firstName": {
                    "type": "string",
                    "description": "First name of the user"
                  },
                  "lastName": {
                    "type": "string",
                    "description": "Last name of the user"
                  },
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user"
                  },
                  "password": {
                    "type": "string",
                    "description": "Password of the user"
                  },
                  "ref": {
                    "type": "string",
                    "description": "Referral code"
                  }
                },
                "required": [
                  "firstName",
                  "lastName",
                  "email",
                  "password"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User registered successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "cookies": {
                      "type": "object",
                      "properties": {
                        "accessToken": {
                          "type": "string",
                          "description": "Access token"
                        },
                        "sessionId": {
                          "type": "string",
                          "description": "Session ID"
                        },
                        "csrfToken": {
                          "type": "string",
                          "description": "CSRF token"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., email already in use)",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/auth/reset": {
      "post": {
        "summary": "Initiates a password reset process for a user",
        "operationId": "resetPassword",
        "tags": [
          "Auth"
        ],
        "description": "Initiates a password reset process for a user and sends an email with a reset link",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user"
                  }
                },
                "required": [
                  "email"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Password reset process initiated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "message": {
                          "type": "string",
                          "description": "Success message"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing email)"
          },
          "404": {
            "description": "User not found with the provided email"
          }
        },
        "security": []
      }
    },
    "/api/auth/role": {
      "get": {
        "summary": "Retrieves all roles",
        "operationId": "getRoles",
        "tags": [
          "Auth"
        ],
        "description": "Retrieves all roles",
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Roles retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "ID of the role"
                      },
                      "name": {
                        "type": "string",
                        "description": "Name of the role"
                      },
                      "permissions": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "ID of the permission"
                            },
                            "name": {
                              "type": "string",
                              "description": "Name of the permission"
                            }
                          },
                          "required": [
                            "id",
                            "name"
                          ]
                        }
                      }
                    },
                    "required": [
                      "id",
                      "name",
                      "permissions"
                    ]
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Role not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/auth/session": {
      "get": {
        "summary": "Retrieves session data by sessionId",
        "operationId": "getSessionData",
        "tags": [
          "Session"
        ],
        "description": "Retrieves session data from Redis by sessionId",
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "Session data retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "string"
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Category not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/auth/verify/email": {
      "post": {
        "summary": "Verifies the email with the provided token",
        "operationId": "verifyEmailToken",
        "tags": [
          "Auth"
        ],
        "description": "Verifies the email with the provided token",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "token": {
                    "type": "string",
                    "description": "The email verification token"
                  }
                },
                "required": [
                  "token"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Email verified successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing or invalid token)"
          },
          "404": {
            "description": "Token not found or expired"
          }
        },
        "security": []
      }
    },
    "/api/auth/verify/reset": {
      "post": {
        "summary": "Verifies a password reset token and sets the new password",
        "operationId": "verifyPasswordReset",
        "tags": [
          "Auth"
        ],
        "description": "Verifies a password reset token and sets the new password",
        "requiresAuth": false,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "token": {
                    "type": "string",
                    "description": "The password reset token"
                  },
                  "newPassword": {
                    "type": "string",
                    "description": "The new password"
                  }
                },
                "required": [
                  "token",
                  "newPassword"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Password reset successfully, new password set",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    },
                    "cookies": {
                      "type": "object",
                      "properties": {
                        "accessToken": {
                          "type": "string",
                          "description": "The new access token"
                        },
                        "refreshToken": {
                          "type": "string",
                          "description": "The new refresh token"
                        },
                        "sessionId": {
                          "type": "string",
                          "description": "The new session ID"
                        },
                        "csrfToken": {
                          "type": "string",
                          "description": "The new CSRF token"
                        }
                      },
                      "required": [
                        "accessToken",
                        "refreshToken",
                        "csrfToken"
                      ]
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing token or newPassword)"
          },
          "401": {
            "description": "Unauthorized or invalid token"
          }
        },
        "security": []
      }
    },
    "/api/content/author/{authorId}/{id}": {
      "del": {
        "summary": "Deletes a specific post",
        "operationId": "deletePost",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 1,
            "name": "id",
            "in": "path",
            "description": "ID of the post to delete",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "restore",
            "in": "query",
            "description": "Restore the post instead of deleting",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "force",
            "in": "query",
            "description": "Delete the post permanently",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Post deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful deletion"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Post not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "Retrieves a single blog post by ID",
        "description": "This endpoint retrieves a single blog post by its ID.",
        "operationId": "getPostById",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 1,
            "name": "id",
            "in": "path",
            "description": "The ID of the blog post to retrieve",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Post ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Blog post retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "string"
                        },
                        "title": {
                          "type": "string"
                        },
                        "content": {
                          "type": "string"
                        },
                        "categoryId": {
                          "type": "string"
                        },
                        "authorId": {
                          "type": "string"
                        },
                        "slug": {
                          "type": "string"
                        },
                        "description": {
                          "type": "string",
                          "nullable": true
                        },
                        "status": {
                          "type": "string",
                          "enum": [
                            "PUBLISHED",
                            "DRAFT",
                            "TRASH"
                          ]
                        },
                        "image": {
                          "type": "string",
                          "nullable": true
                        },
                        "createdAt": {
                          "type": "string",
                          "format": "date-time"
                        },
                        "updatedAt": {
                          "type": "string",
                          "format": "date-time",
                          "nullable": true
                        },
                        "author": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string"
                            },
                            "userId": {
                              "type": "string"
                            }
                          }
                        },
                        "category": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string"
                            },
                            "name": {
                              "type": "string"
                            },
                            "slug": {
                              "type": "string"
                            }
                          }
                        },
                        "postTag": {
                          "type": "array",
                          "items": {
                            "type": "object",
                            "properties": {
                              "id": {
                                "type": "string"
                              },
                              "postId": {
                                "type": "string"
                              },
                              "tagId": {
                                "type": "string"
                              }
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Blog post not found"
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "put": {
        "summary": "Updates a blog post identified by id",
        "description": "This endpoint updates an existing blog post.",
        "operationId": "updatePost",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 1,
            "name": "id",
            "in": "path",
            "description": "The id of the blog post to update",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Post Slug"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "description": "Updated blog post data",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "title": {
                    "type": "string",
                    "description": "Title of the post"
                  },
                  "content": {
                    "type": "string",
                    "description": "Content of the post"
                  },
                  "description": {
                    "type": "string",
                    "description": "Description of the post"
                  },
                  "categoryId": {
                    "type": "string",
                    "description": "Category ID for the post"
                  },
                  "status": {
                    "type": "string",
                    "description": "New status of the blog post",
                    "enum": [
                      "PUBLISHED",
                      "DRAFT"
                    ]
                  },
                  "tags": {
                    "type": "array",
                    "description": "Array of tag names associated with the post",
                    "items": {
                      "type": "string"
                    }
                  }
                },
                "required": [
                  "title",
                  "content",
                  "categoryId",
                  "status"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Blog post updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message of successful author creation"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, user must be authenticated"
          },
          "404": {
            "description": "Blog post not found"
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/author/{authorId}/{id}/status": {
      "put": {
        "summary": "Update Status for a Post",
        "operationId": "updatePostStatus",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "ID of the Post to update",
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "status": {
                    "type": "string",
                    "enum": [
                      "PUBLISHED",
                      "DRAFT",
                      "TRASH"
                    ],
                    "description": "New status to apply to the Post"
                  }
                },
                "required": [
                  "status"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Post updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Post not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/author/{authorId}": {
      "del": {
        "summary": "Bulk deletes posts by IDs",
        "operationId": "bulkDeletePosts",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "parameters": [
          {
            "name": "restore",
            "in": "query",
            "description": "Restore the Posts instead of deleting",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "force",
            "in": "query",
            "description": "Delete the Posts permanently",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "ids": {
                    "type": "array",
                    "items": {
                      "type": "string"
                    },
                    "description": "Array of post IDs to delete"
                  }
                },
                "required": [
                  "ids"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Posts deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Posts not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "List all posts",
        "operationId": "listPosts",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Posts retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "title": {
                            "type": "string",
                            "description": "Title of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "content": {
                            "type": "string",
                            "description": "Content of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "categoryId": {
                            "type": "string",
                            "description": "Category ID linked to the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "slug": {
                            "type": "string",
                            "description": "Slug for the Post URL",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "description": {
                            "type": "string",
                            "description": "Description of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Publication status of the Post",
                            "enum": [
                              "PUBLISHED",
                              "DRAFT",
                              "TRASH"
                            ]
                          },
                          "image": {
                            "type": "string",
                            "description": "Image URL of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "createdAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Creation date of the Post",
                            "nullable": false
                          },
                          "updatedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Last update date of the Post",
                            "nullable": false
                          },
                          "deletedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Deletion date of the Post, if applicable",
                            "nullable": false
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Posts not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Creates a new blog post",
        "description": "This endpoint creates a new blog post.",
        "operationId": "createPost",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "description": "New blog post data",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "title": {
                    "type": "string",
                    "description": "Title of the post"
                  },
                  "content": {
                    "type": "string",
                    "description": "Content of the post"
                  },
                  "description": {
                    "type": "string",
                    "description": "Description of the post"
                  },
                  "categoryId": {
                    "type": "string",
                    "description": "Category ID for the post"
                  },
                  "status": {
                    "type": "string",
                    "description": "Status of the blog post",
                    "enum": [
                      "PUBLISHED",
                      "DRAFT"
                    ]
                  },
                  "tags": {
                    "type": "array",
                    "description": "Array of tag names associated with the post",
                    "items": {
                      "type": "string"
                    }
                  },
                  "slug": {
                    "type": "string",
                    "description": "Slug of the post"
                  }
                },
                "required": [
                  "title",
                  "content",
                  "categoryId",
                  "status",
                  "slug"
                ]
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Blog post created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message of successful post creation"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, user must be authenticated"
          },
          "409": {
            "description": "Conflict, post with the same slug already exists"
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/author/{authorId}/status": {
      "put": {
        "summary": "Bulk updates the status of Posts",
        "operationId": "bulkUpdatePostStatus",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "authorId",
            "in": "path",
            "description": "ID of the author",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "ids": {
                    "type": "array",
                    "description": "Array of Post IDs to update",
                    "items": {
                      "type": "string"
                    }
                  },
                  "status": {
                    "type": "string",
                    "enum": [
                      "PUBLISHED",
                      "DRAFT",
                      "TRASH"
                    ],
                    "description": "New status to apply to the Posts"
                  }
                },
                "required": [
                  "ids",
                  "status"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Post updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Post not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/author/{authorId}/structure": {
      "get": {
        "summary": "Get form structure for Blog Posts",
        "operationId": "getPostStructure",
        "tags": [
          "Content",
          "Author",
          "Post"
        ],
        "responses": {
          "200": {
            "description": "Form structure for managing Blog Posts",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "oneOf": [
                      {
                        "type": "object",
                        "properties": {
                          "type": {
                            "type": "string",
                            "enum": [
                              "input",
                              "select",
                              "switch",
                              "file"
                            ]
                          },
                          "label": {
                            "type": "string"
                          },
                          "name": {
                            "type": "string"
                          },
                          "placeholder": {
                            "type": "string",
                            "nullable": true
                          },
                          "options": {
                            "type": "array",
                            "items": {
                              "type": "string"
                            },
                            "nullable": true
                          },
                          "fileType": {
                            "type": "string",
                            "nullable": true
                          },
                          "width": {
                            "type": "integer",
                            "nullable": true
                          },
                          "height": {
                            "type": "integer",
                            "nullable": true
                          },
                          "maxSize": {
                            "type": "number",
                            "nullable": true
                          },
                          "notNull": {
                            "type": "boolean",
                            "nullable": true
                          },
                          "ts": {
                            "type": "string"
                          }
                        },
                        "required": [
                          "type",
                          "label",
                          "name"
                        ]
                      },
                      {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "type": {
                              "type": "string",
                              "enum": [
                                "input",
                                "select",
                                "switch",
                                "file"
                              ]
                            },
                            "label": {
                              "type": "string"
                            },
                            "name": {
                              "type": "string"
                            },
                            "placeholder": {
                              "type": "string",
                              "nullable": true
                            },
                            "options": {
                              "type": "array",
                              "items": {
                                "type": "string"
                              },
                              "nullable": true
                            },
                            "fileType": {
                              "type": "string",
                              "nullable": true
                            },
                            "width": {
                              "type": "integer",
                              "nullable": true
                            },
                            "height": {
                              "type": "integer",
                              "nullable": true
                            },
                            "maxSize": {
                              "type": "number",
                              "nullable": true
                            },
                            "notNull": {
                              "type": "boolean",
                              "nullable": true
                            },
                            "ts": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "type",
                            "label",
                            "name"
                          ]
                        }
                      }
                    ]
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/author": {
      "get": {
        "summary": "Lists all authors based on status and posts",
        "description": "This endpoint retrieves all available authors based on their status and optionally includes their posts.",
        "operationId": "getAuthors",
        "tags": [
          "Content",
          "Author"
        ],
        "requiresAuth": false,
        "parameters": [
          {
            "name": "status",
            "in": "query",
            "description": "Filter authors by status",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "PENDING",
                "APPROVED",
                "REJECTED"
              ]
            }
          },
          {
            "name": "posts",
            "in": "query",
            "description": "Include posts for each author",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Authors retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Generic ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "userId": {
                        "type": "string",
                        "description": "User ID associated with the entity",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "string",
                        "description": "Current status",
                        "enum": [
                          "PENDING",
                          "APPROVED",
                          "REJECTED"
                        ]
                      },
                      "user": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Generic ID",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "firstName": {
                            "type": "string",
                            "description": "First name of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "lastName": {
                            "type": "string",
                            "description": "Last name of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "avatar": {
                            "type": "string",
                            "description": "Avatar URL of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": true
                          }
                        }
                      },
                      "posts": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "Generic ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "title": {
                              "type": "string",
                              "description": "Title of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "content": {
                              "type": "string",
                              "description": "Content of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "categoryId": {
                              "type": "string",
                              "description": "Generic ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "authorId": {
                              "type": "string",
                              "description": "Generic ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "slug": {
                              "type": "string",
                              "description": "Slug of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "description": {
                              "type": "string",
                              "description": "Description of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": true
                            },
                            "status": {
                              "type": "string",
                              "description": "Post status",
                              "enum": [
                                "PUBLISHED",
                                "DRAFT",
                                "TRASH"
                              ]
                            },
                            "image": {
                              "type": "string",
                              "description": "Image URL of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": true
                            },
                            "createdAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Creation date of the post",
                              "nullable": false
                            },
                            "updatedAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Last update date of the post",
                              "nullable": true
                            }
                          }
                        },
                        "nullable": true
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Author not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      },
      "post": {
        "summary": "Creates a new author",
        "description": "This endpoint creates a new author.",
        "operationId": "createAuthor",
        "tags": [
          "Content",
          "Author"
        ],
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "Author created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/category/{id}": {
      "del": {
        "summary": "Deletes a blog category",
        "description": "This endpoint deletes a blog category.",
        "operationId": "deleteCategory",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the category to delete",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Category ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Category deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful deletion"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Category not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "Retrieves a single category by ID with optional inclusion of posts",
        "description": "This endpoint retrieves a single category by its ID with optional inclusion of posts.",
        "operationId": "getCategoryById",
        "tags": [
          "Blog"
        ],
        "requiresAuth": false,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the category to retrieve",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Category ID"
            }
          },
          {
            "name": "posts",
            "in": "query",
            "description": "Include posts in the category",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Category retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Category ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Name of the category",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "slug": {
                      "type": "string",
                      "description": "Slug for the category",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "image": {
                      "type": "string",
                      "description": "Image URL for the category",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": true
                    },
                    "description": {
                      "type": "string",
                      "description": "Description of the category",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": true
                    },
                    "posts": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Post ID",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "title": {
                            "type": "string",
                            "description": "Title of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "content": {
                            "type": "string",
                            "description": "Content of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "categoryId": {
                            "type": "string",
                            "description": "Category ID of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "authorId": {
                            "type": "string",
                            "description": "Author ID of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "slug": {
                            "type": "string",
                            "description": "Slug of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "description": {
                            "type": "string",
                            "description": "Description of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": true
                          },
                          "status": {
                            "type": "string",
                            "description": "Status of the post",
                            "enum": [
                              "PUBLISHED",
                              "DRAFT",
                              "TRASH"
                            ]
                          },
                          "image": {
                            "type": "string",
                            "description": "Image URL of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": true
                          },
                          "createdAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Creation date of the post",
                            "nullable": false
                          },
                          "updatedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Last update date of the post",
                            "nullable": true
                          }
                        }
                      },
                      "nullable": true
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Category not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      },
      "put": {
        "summary": "Updates an existing blog category",
        "description": "This endpoint updates an existing blog category.",
        "operationId": "updateCategory",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the category to update",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Category ID"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "description": "New name of the category",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "category": {
                    "type": "string",
                    "description": "New name of the category"
                  }
                },
                "required": [
                  "category"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Category updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Category not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/category": {
      "get": {
        "summary": "Lists all categories with optional inclusion of posts",
        "description": "This endpoint retrieves all available categories along with their associated posts.",
        "operationId": "getCategories",
        "tags": [
          "Blog"
        ],
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Categories retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Category ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Name of the category",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "slug": {
                        "type": "string",
                        "description": "Slug for the category",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "image": {
                        "type": "string",
                        "description": "Image URL for the category",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": true
                      },
                      "description": {
                        "type": "string",
                        "description": "Description of the category",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": true
                      },
                      "posts": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "Post ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "title": {
                              "type": "string",
                              "description": "Title of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "content": {
                              "type": "string",
                              "description": "Content of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "categoryId": {
                              "type": "string",
                              "description": "Category ID of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "authorId": {
                              "type": "string",
                              "description": "Author ID of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "slug": {
                              "type": "string",
                              "description": "Slug of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "description": {
                              "type": "string",
                              "description": "Description of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": true
                            },
                            "status": {
                              "type": "string",
                              "description": "Status of the post",
                              "enum": [
                                "PUBLISHED",
                                "DRAFT",
                                "TRASH"
                              ]
                            },
                            "image": {
                              "type": "string",
                              "description": "Image URL of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": true
                            },
                            "createdAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Creation date of the post",
                              "nullable": false
                            },
                            "updatedAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Last update date of the post",
                              "nullable": true
                            }
                          }
                        },
                        "nullable": true
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Category not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      },
      "post": {
        "summary": "Creates a new blog category",
        "description": "This endpoint creates a new blog category.",
        "operationId": "createCategory",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "description": "Name of the category to create",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "category": {
                    "type": "string",
                    "description": "Name of the category to create"
                  }
                },
                "required": [
                  "category"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Category created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/comment/{id}": {
      "del": {
        "summary": "Deletes a blog comment",
        "description": "This endpoint deletes a blog comment.",
        "operationId": "deleteComment",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the comment to delete",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Comment ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Comment deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful deletion"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Comment not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "put": {
        "summary": "Updates an existing blog comment",
        "description": "This endpoint updates an existing blog comment.",
        "operationId": "updateComment",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the comment to update",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Comment ID"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "description": "Comment data to update",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "comment": {
                    "type": "string",
                    "description": "Updated comment content"
                  }
                },
                "required": [
                  "comment"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Comment updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Comment not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/comment/{postId}": {
      "post": {
        "summary": "Creates a new blog comment",
        "description": "This endpoint creates a new blog comment.",
        "operationId": "createComment",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "postId",
            "in": "path",
            "description": "The ID of the post to comment on",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Post ID"
            }
          }
        ],
        "requestBody": {
          "description": "Data for creating a new comment",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "content": {
                    "type": "string",
                    "description": "Name of the comment to create"
                  }
                },
                "required": [
                  "content"
                ]
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "Comment created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/comment": {
      "get": {
        "summary": "Lists all comments with optional inclusion of posts",
        "description": "This endpoint retrieves all available comments along with their associated posts.",
        "operationId": "getComments",
        "tags": [
          "Blog"
        ],
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Comments retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Comment ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Name associated with the comment",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "slug": {
                        "type": "string",
                        "description": "Slug for the comment",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "posts": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "Post ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "content": {
                              "type": "string",
                              "description": "Content of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "userId": {
                              "type": "string",
                              "description": "User ID of the poster",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "postId": {
                              "type": "string",
                              "description": "ID of the post commented on",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "createdAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Creation date of the comment",
                              "nullable": false
                            },
                            "updatedAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Last update date of the comment",
                              "nullable": false
                            },
                            "deletedAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Deletion date of the comment",
                              "nullable": true
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Comments not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/page/{id}": {
      "get": {
        "summary": "Retrieves a single page by ID",
        "description": "Fetches detailed information about a specific page based on its unique identifier.",
        "operationId": "getPage",
        "tags": [
          "Page"
        ],
        "requiresAuth": false,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The ID of the page to retrieve",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Page retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "title": {
                      "type": "string",
                      "description": "Title of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "content": {
                      "type": "string",
                      "description": "Content of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "description": {
                      "type": "string",
                      "description": "Description of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "image": {
                      "type": "string",
                      "description": "Image of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": true
                    },
                    "slug": {
                      "type": "string",
                      "description": "Slug of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Status of the page",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "createdAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Date and time the page was created",
                      "nullable": false
                    },
                    "updatedAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Date and time the page was last updated",
                      "nullable": true
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Page not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/page": {
      "get": {
        "summary": "Lists all pages",
        "description": "Fetches a comprehensive list of all pages available on the platform.",
        "operationId": "listAllPages",
        "tags": [
          "Page"
        ],
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Pages retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object"
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Pages not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/post/{slug}": {
      "get": {
        "summary": "Retrieves a single blog post by ID",
        "description": "This endpoint retrieves a single blog post by its ID.",
        "operationId": "getPostById",
        "tags": [
          "Blog"
        ],
        "requiresAuth": false,
        "parameters": [
          {
            "index": 0,
            "name": "slug",
            "in": "path",
            "description": "The ID of the blog post to retrieve",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Post ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Blog post retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "title": {
                      "type": "string",
                      "description": "Title of the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "content": {
                      "type": "string",
                      "description": "Content of the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "categoryId": {
                      "type": "string",
                      "description": "Category ID linked to the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "authorId": {
                      "type": "string",
                      "description": "Author ID who wrote the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "slug": {
                      "type": "string",
                      "description": "Slug for the Post URL",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "description": {
                      "type": "string",
                      "description": "Description of the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Publication status of the Post",
                      "enum": [
                        "PUBLISHED",
                        "DRAFT",
                        "TRASH"
                      ]
                    },
                    "image": {
                      "type": "string",
                      "description": "Image URL of the Post",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "createdAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Creation date of the Post",
                      "nullable": false
                    },
                    "updatedAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Last update date of the Post",
                      "nullable": false
                    },
                    "deletedAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Deletion date of the Post, if applicable",
                      "nullable": false
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Post not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/post": {
      "get": {
        "summary": "List all posts",
        "operationId": "listPosts",
        "tags": [
          "Posts"
        ],
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Posts retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "title": {
                            "type": "string",
                            "description": "Title of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "content": {
                            "type": "string",
                            "description": "Content of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "categoryId": {
                            "type": "string",
                            "description": "Category ID linked to the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "authorId": {
                            "type": "string",
                            "description": "Author ID who wrote the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "slug": {
                            "type": "string",
                            "description": "Slug for the Post URL",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "description": {
                            "type": "string",
                            "description": "Description of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Publication status of the Post",
                            "enum": [
                              "PUBLISHED",
                              "DRAFT",
                              "TRASH"
                            ]
                          },
                          "image": {
                            "type": "string",
                            "description": "Image URL of the Post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "createdAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Creation date of the Post",
                            "nullable": false
                          },
                          "updatedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Last update date of the Post",
                            "nullable": false
                          },
                          "deletedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Deletion date of the Post, if applicable",
                            "nullable": false
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Posts not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/slider": {
      "get": {
        "summary": "List all sliders",
        "operationId": "listSliders",
        "tags": [
          "Sliders"
        ],
        "responses": {
          "200": {
            "description": "Sliders retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "ID of the Slider",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "image": {
                        "type": "string",
                        "description": "Image URL of the Slider",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "link": {
                        "type": "string",
                        "description": "Link URL of the Slider",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "boolean",
                        "description": "Status of the Slider"
                      },
                      "createdAt": {
                        "type": "string",
                        "format": "date-time",
                        "description": "Creation date of the Slider",
                        "nullable": false
                      },
                      "updatedAt": {
                        "type": "string",
                        "format": "date-time",
                        "description": "Last update date of the Slider",
                        "nullable": false
                      },
                      "deletedAt": {
                        "type": "string",
                        "format": "date-time",
                        "description": "Deletion date of the Slider, if applicable",
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Sliders not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/tag/{id}": {
      "del": {
        "summary": "Deletes a blog tag",
        "description": "This endpoint deletes a blog tag.",
        "operationId": "deleteTag",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the tag to delete",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Tag ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Tag deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful deletion"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Tag not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "put": {
        "summary": "Updates an existing blog tag",
        "description": "This endpoint updates an existing blog tag.",
        "operationId": "updateTag",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the tag to update",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Tag ID"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "description": "New name of the tag",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "tag": {
                    "type": "string",
                    "description": "New name of the tag"
                  }
                },
                "required": [
                  "tag"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Tag updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Tag not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/content/tag/{slug}": {
      "get": {
        "summary": "Retrieves a single tag by slug with optional inclusion of posts",
        "description": "This endpoint retrieves a single tag by its slug with optional inclusion of posts.",
        "operationId": "getTagBySlug",
        "tags": [
          "Blog"
        ],
        "requiresAuth": false,
        "parameters": [
          {
            "index": 0,
            "name": "slug",
            "in": "path",
            "description": "The slug of the tag to retrieve",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "posts",
            "in": "query",
            "description": "Include posts tagged with this tag",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Tag retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Tag ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Name of the tag",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "slug": {
                      "type": "string",
                      "description": "Slug for the tag",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "posts": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Post ID",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "title": {
                            "type": "string",
                            "description": "Title of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "content": {
                            "type": "string",
                            "description": "Content of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "authorId": {
                            "type": "string",
                            "description": "Author ID of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "categoryId": {
                            "type": "string",
                            "description": "Category ID of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "slug": {
                            "type": "string",
                            "description": "Slug of the post",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "createdAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Creation date of the post",
                            "nullable": false
                          },
                          "updatedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Last update date of the post",
                            "nullable": true
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Tag not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/content/tag": {
      "get": {
        "summary": "Lists all tags with optional inclusion of posts",
        "description": "This endpoint retrieves all available tags along with their associated posts.",
        "operationId": "getTags",
        "tags": [
          "Blog"
        ],
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Tags retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Tag ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Name of the tag",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "slug": {
                        "type": "string",
                        "description": "Slug for the tag",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "posts": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "Post ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "title": {
                              "type": "string",
                              "description": "Title of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "content": {
                              "type": "string",
                              "description": "Content of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "authorId": {
                              "type": "string",
                              "description": "Author ID of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "categoryId": {
                              "type": "string",
                              "description": "Category ID of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "slug": {
                              "type": "string",
                              "description": "Slug of the post",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "createdAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Creation date of the post",
                              "nullable": false
                            },
                            "updatedAt": {
                              "type": "string",
                              "format": "date-time",
                              "description": "Last update date of the post",
                              "nullable": true
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Tag not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      },
      "post": {
        "summary": "Creates a new blog tag",
        "description": "This endpoint creates a new blog tag.",
        "operationId": "createTag",
        "tags": [
          "Blog"
        ],
        "requiresAuth": true,
        "requestBody": {
          "description": "Data for creating a new tag",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "tag": {
                    "type": "string",
                    "description": "Name of the tag to create"
                  }
                },
                "required": [
                  "tag"
                ]
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "Tag created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/exchange/binary/order/{id}": {
      "del": {
        "summary": "Cancel Binary Order",
        "operationId": "cancelBinaryOrder",
        "tags": [
          "Binary",
          "Orders"
        ],
        "description": "Cancels a binary order for the authenticated user.",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "description": "ID of the binary order to cancel.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "description": "Cancellation percentage data.",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "percentage": {
                    "type": "number"
                  }
                }
              }
            }
          },
          "required": false
        },
        "responses": {
          "200": {
            "description": "Binary order cancelled",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Binary Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      },
      "get": {
        "summary": "Show Binary Order",
        "operationId": "showBinaryOrder",
        "tags": [
          "Binary",
          "Orders"
        ],
        "description": "Retrieves a specific binary order by ID for the authenticated user.",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "description": "ID of the binary order to retrieve.",
            "required": true,
            "schema": {
              "type": "string",
              "format": "uuid"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Binary order data",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the binary order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false,
                      "expectedFormat": "uuid"
                    },
                    "userId": {
                      "type": "string",
                      "description": "User ID associated with the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "symbol": {
                      "type": "string",
                      "description": "Trading symbol",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "price": {
                      "type": "number",
                      "description": "Entry price of the order",
                      "nullable": false
                    },
                    "amount": {
                      "type": "number",
                      "description": "Amount of the order",
                      "nullable": false
                    },
                    "profit": {
                      "type": "number",
                      "description": "Profit from the order",
                      "nullable": false
                    },
                    "side": {
                      "type": "string",
                      "description": "Side of the order (e.g., BUY, SELL)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "type": {
                      "type": "string",
                      "description": "Type of order (e.g., LIMIT, MARKET)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "barrier": {
                      "type": "number",
                      "description": "Barrier price of the order",
                      "nullable": true
                    },
                    "strikePrice": {
                      "type": "number",
                      "description": "Strike price of the order",
                      "nullable": true
                    },
                    "payoutPerPoint": {
                      "type": "number",
                      "description": "Payout per point of the order",
                      "nullable": true
                    },
                    "status": {
                      "type": "string",
                      "description": "Status of the order (e.g., OPEN, CLOSED)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "isDemo": {
                      "type": "boolean",
                      "description": "Whether the order is a demo"
                    },
                    "closedAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Time when the order was closed",
                      "nullable": true
                    },
                    "closePrice": {
                      "type": "number",
                      "description": "Price at which the order was closed",
                      "nullable": false
                    },
                    "createdAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Creation date of the order",
                      "nullable": false
                    },
                    "updatedAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Last update date of the order",
                      "nullable": true
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Binary Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/binary/order": {
      "get": {
        "summary": "List Orders",
        "operationId": "listOrders",
        "tags": [
          "Exchange",
          "Orders"
        ],
        "description": "Retrieves a list of orders for the authenticated user.",
        "parameters": [
          {
            "name": "type",
            "in": "query",
            "description": "Type of order to retrieve.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "currency",
            "in": "query",
            "description": "currency of the order to retrieve.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "pair",
            "in": "query",
            "description": "pair of the order to retrieve.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "A list of orders",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {}
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Create Binary Order",
        "operationId": "createBinaryOrder",
        "tags": [
          "Binary",
          "Orders"
        ],
        "description": "Creates a new binary order for the authenticated user.",
        "requestBody": {
          "description": "Binary order data to be created.",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "currency": {
                    "type": "string"
                  },
                  "pair": {
                    "type": "string"
                  },
                  "amount": {
                    "type": "number"
                  },
                  "side": {
                    "type": "string"
                  },
                  "closedAt": {
                    "type": "string",
                    "format": "date-time"
                  },
                  "isDemo": {
                    "type": "boolean"
                  },
                  "type": {
                    "type": "string"
                  }
                },
                "required": [
                  "currency",
                  "pair",
                  "amount",
                  "side",
                  "closedAt",
                  "type"
                ]
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "Binary Order created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/exchange/binary/order/last": {
      "get": {
        "summary": "List Binary Orders from Last 30 Days",
        "operationId": "listBinaryOrdersLast30Days",
        "tags": [
          "Binary",
          "Orders"
        ],
        "description": "Retrieves the non-pending binary orders for practice and non-practice accounts from the last 30 days and compares them with the previous month.",
        "responses": {
          "200": {
            "description": "A list of binary orders from the last 30 days",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "practiceOrders": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {}
                      }
                    },
                    "nonPracticeOrders": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {}
                      }
                    },
                    "livePercentageChange": {
                      "type": "number"
                    },
                    "practicePercentageChange": {
                      "type": "number"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/exchange/chart": {
      "get": {
        "summary": "Get Historical Chart Data",
        "operationId": "getHistoricalChartData",
        "tags": [
          "Chart",
          "Historical"
        ],
        "description": "Retrieves historical chart data for the authenticated user.",
        "parameters": [
          {
            "name": "symbol",
            "in": "query",
            "description": "Symbol to retrieve data for.",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "interval",
            "in": "query",
            "description": "Interval to retrieve data for.",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "from",
            "in": "query",
            "description": "Start timestamp to retrieve data from.",
            "required": true,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "to",
            "in": "query",
            "description": "End timestamp to retrieve data from.",
            "required": true,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "duration",
            "in": "query",
            "description": "Duration to retrieve data for.",
            "required": true,
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Historical chart data retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "timestamp": {
                        "type": "number",
                        "description": "Timestamp for the data point",
                        "nullable": false
                      },
                      "open": {
                        "type": "number",
                        "description": "Opening price for the data interval",
                        "nullable": false
                      },
                      "high": {
                        "type": "number",
                        "description": "Highest price during the data interval",
                        "nullable": false
                      },
                      "low": {
                        "type": "number",
                        "description": "Lowest price during the data interval",
                        "nullable": false
                      },
                      "close": {
                        "type": "number",
                        "description": "Closing price for the data interval",
                        "nullable": false
                      },
                      "volume": {
                        "type": "number",
                        "description": "Volume of trades during the data interval",
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Chart not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/currency/{id}": {
      "get": {
        "summary": "Show Currency",
        "operationId": "getCurrency",
        "tags": [
          "Currencies"
        ],
        "description": "Retrieves details of a specific currency by ID.",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "description": "ID of the currency to retrieve.",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Currency details",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Unique identifier for the currency",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "currency": {
                      "type": "string",
                      "description": "Currency code (e.g., USD, EUR)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Full name of the currency",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "precision": {
                      "type": "number",
                      "description": "Number of decimal places used by the currency",
                      "nullable": false
                    },
                    "price": {
                      "type": "number",
                      "description": "Current price of the currency in USD",
                      "nullable": false
                    },
                    "status": {
                      "type": "boolean",
                      "description": "Active status of the currency"
                    },
                    "chains": {
                      "type": "object",
                      "description": "Blockchain networks supported by the currency",
                      "additionalProperties": {
                        "type": "object",
                        "properties": {
                          "network": {
                            "type": "string",
                            "description": "Network name",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "protocol": {
                            "type": "string",
                            "description": "Protocol used",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/currency": {
      "get": {
        "summary": "List Currencies",
        "operationId": "getCurrencies",
        "tags": [
          "Currencies"
        ],
        "description": "Retrieves a list of all currencies.",
        "responses": {
          "200": {
            "description": "A list of currencies",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Unique identifier for the currency",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "currency": {
                        "type": "string",
                        "description": "Currency code (e.g., USD, EUR)",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Full name of the currency",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "precision": {
                        "type": "number",
                        "description": "Number of decimal places used by the currency",
                        "nullable": false
                      },
                      "price": {
                        "type": "number",
                        "description": "Current price of the currency in USD",
                        "nullable": false
                      },
                      "status": {
                        "type": "boolean",
                        "description": "Active status of the currency"
                      },
                      "chains": {
                        "type": "object",
                        "description": "Blockchain networks supported by the currency",
                        "additionalProperties": {
                          "type": "object",
                          "properties": {
                            "network": {
                              "type": "string",
                              "description": "Network name",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "protocol": {
                              "type": "string",
                              "description": "Protocol used",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/market/{id}": {
      "get": {
        "summary": "Show Market Details",
        "operationId": "showMarket",
        "tags": [
          "Exchange",
          "Markets"
        ],
        "description": "Retrieves details of a specific market by ID.",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The ID of the market to retrieve.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Market details",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Unique identifier for the market",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "currency": {
                      "type": "string",
                      "description": "Primary currency of the market",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "pair": {
                      "type": "string",
                      "description": "Currency pair traded in this market",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "isTrending": {
                      "type": "boolean",
                      "description": "Indicator if the market is currently trending"
                    },
                    "isHot": {
                      "type": "boolean",
                      "description": "Indicator if the market is currently considered 'hot'"
                    },
                    "metadata": {
                      "type": "object",
                      "description": "Additional metadata about the market",
                      "additionalProperties": true
                    },
                    "status": {
                      "type": "boolean",
                      "description": "Active status of the market"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Market not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/market": {
      "get": {
        "summary": "List Exchange Markets",
        "operationId": "listMarkets",
        "tags": [
          "Exchange",
          "Markets"
        ],
        "description": "Retrieves a list of all available markets.",
        "parameters": [
          {
            "name": "eco",
            "in": "query",
            "required": true,
            "description": "include eco",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "A list of markets",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Unique identifier for the market",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "currency": {
                        "type": "string",
                        "description": "Primary currency of the market",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "pair": {
                        "type": "string",
                        "description": "Currency pair traded in this market",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "isTrending": {
                        "type": "boolean",
                        "description": "Indicator if the market is currently trending"
                      },
                      "isHot": {
                        "type": "boolean",
                        "description": "Indicator if the market is currently considered 'hot'"
                      },
                      "metadata": {
                        "type": "object",
                        "description": "Additional metadata about the market",
                        "additionalProperties": true
                      },
                      "status": {
                        "type": "boolean",
                        "description": "Active status of the market"
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Market not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/order/{id}": {
      "del": {
        "summary": "Cancel Order",
        "operationId": "cancelOrder",
        "tags": [
          "Exchange",
          "Orders"
        ],
        "description": "Cancels a specific order for the authenticated user.",
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "ID of the order to cancel.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Order canceled successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "example": "Order canceled successfully"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "Show Order Details",
        "operationId": "showOrder",
        "tags": [
          "Exchange",
          "Orders"
        ],
        "description": "Retrieves details of a specific order by ID for the authenticated user.",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "description": "ID of the order to retrieve.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Order details",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Unique identifier for the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "referenceId": {
                      "type": "string",
                      "description": "External reference ID for the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "userId": {
                      "type": "string",
                      "description": "User ID associated with the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Status of the order (e.g., pending, completed)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "symbol": {
                      "type": "string",
                      "description": "Trading symbol for the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "type": {
                      "type": "string",
                      "description": "Type of order (e.g., market, limit)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "timeInForce": {
                      "type": "string",
                      "description": "Time in force policy for the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "side": {
                      "type": "string",
                      "description": "Order side (buy or sell)",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "price": {
                      "type": "number",
                      "description": "Price per unit",
                      "nullable": false
                    },
                    "average": {
                      "type": "number",
                      "description": "Average price per unit",
                      "nullable": false
                    },
                    "amount": {
                      "type": "number",
                      "description": "Total amount ordered",
                      "nullable": false
                    },
                    "filled": {
                      "type": "number",
                      "description": "Amount filled",
                      "nullable": false
                    },
                    "remaining": {
                      "type": "number",
                      "description": "Amount remaining",
                      "nullable": false
                    },
                    "cost": {
                      "type": "number",
                      "description": "Total cost",
                      "nullable": false
                    },
                    "trades": {
                      "type": "object",
                      "description": "Details of trades executed for this order",
                      "additionalProperties": true
                    },
                    "fee": {
                      "type": "number",
                      "description": "Transaction fee",
                      "nullable": false
                    },
                    "feeCurrency": {
                      "type": "string",
                      "description": "Currency of the transaction fee",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "createdAt": {
                      "type": "string",
                      "description": "Creation date of the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "updatedAt": {
                      "type": "string",
                      "description": "Last update date of the order",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/order": {
      "get": {
        "summary": "List Orders",
        "operationId": "listOrders",
        "tags": [
          "Exchange",
          "Orders"
        ],
        "description": "Retrieves a list of orders for the authenticated user.",
        "parameters": [
          {
            "name": "type",
            "in": "query",
            "description": "Type of order to retrieve.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "currency",
            "in": "query",
            "description": "currency of the order to retrieve.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "pair",
            "in": "query",
            "description": "pair of the order to retrieve.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "A list of orders",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Unique identifier for the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "referenceId": {
                        "type": "string",
                        "description": "External reference ID for the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "userId": {
                        "type": "string",
                        "description": "User ID associated with the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "string",
                        "description": "Status of the order (e.g., pending, completed)",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "symbol": {
                        "type": "string",
                        "description": "Trading symbol for the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "type": {
                        "type": "string",
                        "description": "Type of order (e.g., market, limit)",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "timeInForce": {
                        "type": "string",
                        "description": "Time in force policy for the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "side": {
                        "type": "string",
                        "description": "Order side (buy or sell)",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "price": {
                        "type": "number",
                        "description": "Price per unit",
                        "nullable": false
                      },
                      "average": {
                        "type": "number",
                        "description": "Average price per unit",
                        "nullable": false
                      },
                      "amount": {
                        "type": "number",
                        "description": "Total amount ordered",
                        "nullable": false
                      },
                      "filled": {
                        "type": "number",
                        "description": "Amount filled",
                        "nullable": false
                      },
                      "remaining": {
                        "type": "number",
                        "description": "Amount remaining",
                        "nullable": false
                      },
                      "cost": {
                        "type": "number",
                        "description": "Total cost",
                        "nullable": false
                      },
                      "trades": {
                        "type": "object",
                        "description": "Details of trades executed for this order",
                        "additionalProperties": true
                      },
                      "fee": {
                        "type": "number",
                        "description": "Transaction fee",
                        "nullable": false
                      },
                      "feeCurrency": {
                        "type": "string",
                        "description": "Currency of the transaction fee",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "createdAt": {
                        "type": "string",
                        "description": "Creation date of the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "updatedAt": {
                        "type": "string",
                        "description": "Last update date of the order",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Create Order",
        "operationId": "createOrder",
        "tags": [
          "Exchange",
          "Orders"
        ],
        "description": "Creates a new order for the authenticated user.",
        "requestBody": {
          "description": "Order creation data.",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "currency": {
                    "type": "string",
                    "description": "Currency symbol (e.g., BTC)"
                  },
                  "pair": {
                    "type": "string",
                    "description": "Pair symbol (e.g., USDT)"
                  },
                  "type": {
                    "type": "string",
                    "description": "Order type (e.g., limit, market)"
                  },
                  "side": {
                    "type": "string",
                    "description": "Order side (buy or sell)"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Order amount"
                  },
                  "price": {
                    "type": "number",
                    "description": "Order price, required for limit orders"
                  }
                },
                "required": [
                  "currency",
                  "pair",
                  "type",
                  "side",
                  "amount"
                ]
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "Order created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/exchange/orderbook/{currency}/{pair}": {
      "get": {
        "summary": "Get Market Order Book",
        "operationId": "getMarketOrderBook",
        "tags": [
          "Exchange",
          "Markets"
        ],
        "description": "Retrieves the order book for a specific market pair.",
        "parameters": [
          {
            "name": "currency",
            "in": "path",
            "description": "Currency symbol",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "pair",
            "in": "path",
            "description": "Pair symbol",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "limit",
            "in": "query",
            "description": "Limit the number of order book entries",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Order book information",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "asks": {
                      "type": "array",
                      "items": {
                        "type": "array",
                        "items": {
                          "type": "number",
                          "description": "Order book entry consisting of price and volume"
                        }
                      },
                      "description": "Asks are sell orders in the order book"
                    },
                    "bids": {
                      "type": "array",
                      "items": {
                        "type": "array",
                        "items": {
                          "type": "number",
                          "description": "Order book entry consisting of price and volume"
                        }
                      },
                      "description": "Bids are buy orders in the order book"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Orderbook not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/ticker/{currency}/{pair}": {
      "get": {
        "summary": "Get Market Ticker",
        "operationId": "getMarketTicker",
        "tags": [
          "Exchange",
          "Markets"
        ],
        "description": "Retrieves ticker information for a specific market pair.",
        "parameters": [
          {
            "name": "currency",
            "in": "path",
            "required": true,
            "description": "The base currency of the market pair.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "pair",
            "in": "path",
            "required": true,
            "description": "The quote currency of the market pair.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Ticker information",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "symbol": {
                      "type": "string",
                      "description": "Trading symbol for the market pair",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "bid": {
                      "type": "number",
                      "description": "Current highest bid price",
                      "nullable": false
                    },
                    "ask": {
                      "type": "number",
                      "description": "Current lowest ask price",
                      "nullable": false
                    },
                    "close": {
                      "type": "number",
                      "description": "Last close price",
                      "nullable": false
                    },
                    "last": {
                      "type": "number",
                      "description": "Most recent transaction price",
                      "nullable": false
                    },
                    "change": {
                      "type": "number",
                      "description": "Price change percentage",
                      "nullable": false
                    },
                    "baseVolume": {
                      "type": "number",
                      "description": "Volume of base currency traded",
                      "nullable": false
                    },
                    "quoteVolume": {
                      "type": "number",
                      "description": "Volume of quote currency traded",
                      "nullable": false
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ticker not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/ticker": {
      "get": {
        "summary": "Get All Market Tickers",
        "operationId": "getAllMarketTickers",
        "tags": [
          "Exchange",
          "Markets"
        ],
        "description": "Retrieves ticker information for all available market pairs.",
        "responses": {
          "200": {
            "description": "All market tickers information",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "symbol": {
                      "type": "string",
                      "description": "Trading symbol for the market pair",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "bid": {
                      "type": "number",
                      "description": "Current highest bid price",
                      "nullable": false
                    },
                    "ask": {
                      "type": "number",
                      "description": "Current lowest ask price",
                      "nullable": false
                    },
                    "close": {
                      "type": "number",
                      "description": "Last close price",
                      "nullable": false
                    },
                    "last": {
                      "type": "number",
                      "description": "Most recent transaction price",
                      "nullable": false
                    },
                    "change": {
                      "type": "number",
                      "description": "Price change percentage",
                      "nullable": false
                    },
                    "baseVolume": {
                      "type": "number",
                      "description": "Volume of base currency traded",
                      "nullable": false
                    },
                    "quoteVolume": {
                      "type": "number",
                      "description": "Volume of quote currency traded",
                      "nullable": false
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ticker not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/exchange/watchlist": {
      "del": {
        "summary": "Remove Item from Watchlist",
        "operationId": "removeWatchlistItem",
        "tags": [
          "Exchange",
          "Watchlist"
        ],
        "description": "Removes an item from the watchlist for the authenticated user.",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "description": "ID of the watchlist item to remove.",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Watchlist deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful deletion"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Watchlist not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "List Watchlist Items",
        "operationId": "listWatchlistItems",
        "tags": [
          "Exchange",
          "Watchlist"
        ],
        "description": "Retrieves a list of watchlist items for the authenticated user.",
        "responses": {
          "200": {
            "description": "A list of watchlist items",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Unique identifier for the watchlist item",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false,
                        "expectedFormat": "uuid"
                      },
                      "userId": {
                        "type": "string",
                        "description": "User ID associated with the watchlist item",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false,
                        "expectedFormat": "uuid"
                      },
                      "symbol": {
                        "type": "string",
                        "description": "Symbol of the watchlist item",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Watchlist not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Add Item to Watchlist",
        "operationId": "addWatchlistItem",
        "tags": [
          "Exchange",
          "Watchlist"
        ],
        "description": "Adds a new item to the watchlist for the authenticated user.",
        "requestBody": {
          "description": "Data for the watchlist item to add.",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "symbol": {
                    "type": "string",
                    "description": "Symbol of the watchlist item"
                  }
                },
                "required": [
                  "symbol"
                ]
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "Watchlist created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ecosystem/chart": {
      "get": {
        "summary": "Retrieves historical data for a specific symbol",
        "description": "Fetches historical price data based on the specified interval and date range.",
        "operationId": "getHistoricalData",
        "tags": [
          "Market",
          "Historical"
        ],
        "parameters": [
          {
            "name": "symbol",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Trading symbol, e.g., BTC/USD"
            }
          },
          {
            "name": "from",
            "in": "query",
            "required": true,
            "schema": {
              "type": "number",
              "description": "Start timestamp for historical data"
            }
          },
          {
            "name": "to",
            "in": "query",
            "required": true,
            "schema": {
              "type": "number",
              "description": "End timestamp for historical data"
            }
          },
          {
            "name": "interval",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Time interval for the data, e.g., 1m, 5m, 1h"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Historical data retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "openTime": {
                        "type": "number",
                        "description": "Open time of the candle",
                        "nullable": false
                      },
                      "closeTime": {
                        "type": "number",
                        "description": "Close time of the candle",
                        "nullable": false
                      },
                      "open": {
                        "type": "string",
                        "description": "Opening price",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "high": {
                        "type": "string",
                        "description": "Highest price",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "low": {
                        "type": "string",
                        "description": "Lowest price",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "close": {
                        "type": "string",
                        "description": "Closing price",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "volume": {
                        "type": "string",
                        "description": "Volume",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Chart not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/deposit/unlock": {
      "get": {
        "summary": "Unlocks a specific deposit address",
        "description": "Allows administrative unlocking of a custodial wallet deposit address to make it available for reuse.",
        "operationId": "unlockDepositAddress",
        "tags": [
          "Wallet",
          "Deposit"
        ],
        "parameters": [
          {
            "name": "address",
            "in": "query",
            "description": "The deposit address to unlock",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Deposit address unlocked successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message indicating the address has been unlocked."
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ecosystem/market/{id}": {
      "get": {
        "summary": "Retrieves a specific ecosystem market",
        "description": "Fetches details of a specific market in the ecosystem.",
        "operationId": "getEcosystemMarket",
        "tags": [
          "Ecosystem",
          "Markets"
        ],
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "number",
              "description": "Market ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Market details retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "number",
                      "description": "Market ID",
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Market name",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "boolean",
                      "description": "Market status"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Market not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/market": {
      "get": {
        "summary": "Retrieves all ecosystem markets",
        "description": "Fetches a list of all active markets available in the ecosystem.",
        "operationId": "listEcosystemMarkets",
        "tags": [
          "Ecosystem",
          "Markets"
        ],
        "responses": {
          "200": {
            "description": "Markets retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "number",
                        "description": "Market ID",
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Market name",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "boolean",
                        "description": "Market status"
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Market not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/order/{id}": {
      "del": {
        "summary": "Cancels an existing trading order",
        "description": "Cancels an open trading order and refunds the unfulfilled amount, including fee adjustments for partial fills.",
        "operationId": "cancelOrder",
        "tags": [
          "Trading",
          "Orders"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "UUID of the order"
            }
          },
          {
            "name": "timestamp",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Timestamp of the order"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Order cancelled successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ecosystem/order": {
      "get": {
        "summary": "List Orders",
        "operationId": "listOrders",
        "tags": [
          "Exchange",
          "Orders"
        ],
        "description": "Retrieves a list of orders for the authenticated user.",
        "parameters": [
          {
            "name": "type",
            "in": "query",
            "description": "Type of order to retrieve.",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "symbol",
            "in": "query",
            "description": "Symbol of the order to retrieve.",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "A list of orders",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Order ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "symbol": {
                        "type": "string",
                        "description": "Trading symbol",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "type": {
                        "type": "string",
                        "description": "Order type",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "side": {
                        "type": "string",
                        "description": "Order side (buy/sell)",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "amount": {
                        "type": "string",
                        "description": "Order amount, converted from bigint",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "price": {
                        "type": "string",
                        "description": "Order price, converted from bigint",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "cost": {
                        "type": "string",
                        "description": "Total cost, converted from bigint",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "fee": {
                        "type": "string",
                        "description": "Order fee, converted from bigint",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "filled": {
                        "type": "string",
                        "description": "Filled amount, converted from bigint",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "remaining": {
                        "type": "string",
                        "description": "Remaining amount, converted from bigint",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "string",
                        "description": "Order status",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Order not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Creates a new trading order",
        "description": "Submits a new trading order for the logged-in user.",
        "operationId": "createOrder",
        "tags": [
          "Trading",
          "Orders"
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "currency": {
                    "type": "string",
                    "description": "Currency symbol (e.g., BTC)"
                  },
                  "pair": {
                    "type": "string",
                    "description": "Pair symbol (e.g., USDT)"
                  },
                  "type": {
                    "type": "string",
                    "description": "Order type, limit or market"
                  },
                  "side": {
                    "type": "string",
                    "description": "Order side, buy or sell"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount of the order"
                  },
                  "price": {
                    "type": "number",
                    "description": "Price of the order (required if limit)"
                  }
                },
                "required": [
                  "currency",
                  "pair",
                  "type",
                  "side",
                  "amount"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Order created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ecosystem/token/{currency}": {
      "get": {
        "summary": "Retrieves a specific ecosystem token",
        "description": "Fetches details of a specific token in the ecosystem.",
        "operationId": "getEcosystemToken",
        "tags": [
          "Ecosystem",
          "Tokens"
        ],
        "parameters": [
          {
            "name": "chain",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Blockchain chain name"
            }
          },
          {
            "name": "currency",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Currency code of the token"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Token details retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "name": {
                      "type": "string",
                      "description": "Token name",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "currency": {
                      "type": "string",
                      "description": "Token currency code",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "chain": {
                      "type": "string",
                      "description": "Blockchain chain name",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "type": {
                      "type": "string",
                      "description": "Token type",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "boolean",
                      "description": "Token status"
                    },
                    "precision": {
                      "type": "number",
                      "description": "Token precision",
                      "nullable": false
                    },
                    "limits": {
                      "type": "object",
                      "description": "Token transfer limits"
                    },
                    "decimals": {
                      "type": "number",
                      "description": "Token decimal places",
                      "nullable": false
                    },
                    "icon": {
                      "type": "string",
                      "description": "Token icon URL",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": true
                    },
                    "contractType": {
                      "type": "string",
                      "description": "Type of token contract",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "network": {
                      "type": "string",
                      "description": "Network type",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "fee": {
                      "type": "object",
                      "description": "Token fee"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Token not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/token": {
      "get": {
        "summary": "Retrieves all ecosystem tokens",
        "description": "Fetches a list of all active tokens available in the ecosystem.",
        "operationId": "listEcosystemTokens",
        "tags": [
          "Ecosystem",
          "Tokens"
        ],
        "responses": {
          "200": {
            "description": "Tokens retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "name": {
                        "type": "string",
                        "description": "Token name",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "currency": {
                        "type": "string",
                        "description": "Token currency code",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "chain": {
                        "type": "string",
                        "description": "Blockchain chain name",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "type": {
                        "type": "string",
                        "description": "Token type",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "boolean",
                        "description": "Token status"
                      },
                      "precision": {
                        "type": "number",
                        "description": "Token precision",
                        "nullable": false
                      },
                      "limits": {
                        "type": "object",
                        "description": "Token transfer limits"
                      },
                      "decimals": {
                        "type": "number",
                        "description": "Token decimal places",
                        "nullable": false
                      },
                      "icon": {
                        "type": "string",
                        "description": "Token icon URL",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": true
                      },
                      "contractType": {
                        "type": "string",
                        "description": "Type of token contract",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "network": {
                        "type": "string",
                        "description": "Network type",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "fee": {
                        "type": "object",
                        "description": "Token fee"
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Token not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/wallet/{currency}": {
      "get": {
        "summary": "Fetches a specific wallet by currency",
        "description": "Retrieves details of a wallet associated with the logged-in user by its currency.",
        "operationId": "getWallet",
        "tags": [
          "Wallet",
          "User"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "currency",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Currency of the wallet"
            }
          },
          {
            "name": "contractType",
            "in": "query",
            "schema": {
              "type": "string",
              "description": "Chain of the wallet address"
            }
          },
          {
            "name": "chain",
            "in": "query",
            "schema": {
              "type": "string",
              "description": "Chain of the wallet address"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Wallet retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Wallet ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "type": {
                      "type": "string",
                      "description": "Wallet type",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "currency": {
                      "type": "string",
                      "description": "Wallet currency",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "balance": {
                      "type": "number",
                      "description": "Wallet balance",
                      "nullable": false
                    },
                    "transactions": {
                      "type": "array",
                      "description": "List of transactions",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Transaction ID",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "type": {
                            "type": "string",
                            "description": "Transaction type",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Transaction status",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "amount": {
                            "type": "number",
                            "description": "Transaction amount",
                            "nullable": false
                          },
                          "fee": {
                            "type": "number",
                            "description": "Transaction fee",
                            "nullable": false
                          },
                          "description": {
                            "type": "string",
                            "description": "Transaction description",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "metadata": {
                            "type": "object",
                            "description": "Additional metadata for the transaction"
                          },
                          "referenceId": {
                            "type": "string",
                            "description": "Reference ID",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "createdAt": {
                            "type": "string",
                            "description": "Creation time of the transaction",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false,
                            "pattern": "date-time"
                          }
                        },
                        "nullable": true
                      }
                    },
                    "address": {
                      "type": "array",
                      "description": "Wallet addresses",
                      "items": {
                        "type": "string",
                        "description": "Wallet address",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "nullable": true
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ecosystem/wallet/{id}/transfer": {
      "post": {
        "summary": "Transfers funds between user wallets",
        "description": "Allows a user to transfer funds to another user's wallet.",
        "operationId": "transferFunds",
        "tags": [
          "Wallet",
          "Transfer"
        ],
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "UUID of the recipient's wallet or user"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "amount": {
                    "type": "number",
                    "description": "Amount to transfer"
                  },
                  "currency": {
                    "type": "string",
                    "description": "Currency for the transfer"
                  }
                },
                "required": [
                  "amount",
                  "currency"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Transfer completed successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message indicating the transfer has been processed."
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/wallet": {
      "get": {
        "summary": "Lists all wallets for the logged-in user",
        "description": "Retrieves all wallets associated with the logged-in user, optionally including transactions and address.",
        "operationId": "listWallets",
        "tags": [
          "Wallet",
          "User"
        ],
        "parameters": [
          {
            "name": "transactions",
            "in": "query",
            "schema": {
              "type": "boolean",
              "default": false
            },
            "description": "Whether to include transaction details"
          },
          {
            "name": "address",
            "in": "query",
            "schema": {
              "type": "boolean",
              "default": false
            },
            "description": "Whether to include wallet address"
          }
        ],
        "responses": {
          "200": {
            "description": "Wallets retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "Wallet ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "type": {
                        "type": "string",
                        "description": "Wallet type",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "currency": {
                        "type": "string",
                        "description": "Wallet currency",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "balance": {
                        "type": "number",
                        "description": "Wallet balance",
                        "nullable": false
                      },
                      "transactions": {
                        "type": "array",
                        "description": "List of transactions",
                        "items": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "Transaction ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "type": {
                              "type": "string",
                              "description": "Transaction type",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "status": {
                              "type": "string",
                              "description": "Transaction status",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "amount": {
                              "type": "number",
                              "description": "Transaction amount",
                              "nullable": false
                            },
                            "fee": {
                              "type": "number",
                              "description": "Transaction fee",
                              "nullable": false
                            },
                            "description": {
                              "type": "string",
                              "description": "Transaction description",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "metadata": {
                              "type": "object",
                              "description": "Additional metadata for the transaction"
                            },
                            "referenceId": {
                              "type": "string",
                              "description": "Reference ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "createdAt": {
                              "type": "string",
                              "description": "Creation time of the transaction",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false,
                              "pattern": "date-time"
                            }
                          },
                          "nullable": true
                        }
                      },
                      "address": {
                        "type": "array",
                        "description": "Wallet addresses",
                        "items": {
                          "type": "string",
                          "description": "Wallet address",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "nullable": true
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ecosystem/withdraw": {
      "post": {
        "summary": "Withdraws funds to an external address",
        "description": "Processes a withdrawal from the user's wallet to an external address.",
        "operationId": "withdrawFunds",
        "tags": [
          "Wallet",
          "Withdrawal"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "currency": {
                    "type": "string",
                    "description": "Currency to withdraw"
                  },
                  "chain": {
                    "type": "string",
                    "description": "Withdraw method ID"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount to withdraw"
                  },
                  "toAddress": {
                    "type": "string",
                    "description": "Withdraw toAddress"
                  }
                },
                "required": [
                  "currency",
                  "chain",
                  "amount",
                  "toAddress"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Withdrawal processed successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message indicating the withdrawal has been processed."
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ico/contribution/{id}": {
      "get": {
        "summary": "Retrieves a specific ICO contribution",
        "description": "Fetches details of a specific ICO contribution by ID.",
        "operationId": "getIcoContribution",
        "tags": [
          "ICO",
          "Contributions"
        ],
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Contribution ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Contribution retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Contribution ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "userId": {
                      "type": "string",
                      "description": "User ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "phaseId": {
                      "type": "string",
                      "description": "Phase ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "amount": {
                      "type": "number",
                      "description": "Contributed amount",
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Contribution status",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "phase": {
                      "type": "object",
                      "properties": {
                        "token": {
                          "type": "object",
                          "properties": {
                            "id": {
                              "type": "string",
                              "description": "Token ID",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            },
                            "name": {
                              "type": "string",
                              "description": "Token name",
                              "maxLength": 255,
                              "minLength": 0,
                              "nullable": false
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ico Contribution not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ico/contribution": {
      "get": {
        "summary": "Retrieves all contributions made by a user",
        "description": "Fetches a list of all contributions made by the currently logged-in user.",
        "operationId": "listUserContributions",
        "tags": [
          "ICO",
          "Contributions"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "List of ICO Contributions with pagination information",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the ICO Contribution",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "userId": {
                            "type": "string",
                            "description": "ID of the User",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "phaseId": {
                            "type": "string",
                            "description": "ID of the ICO Phase",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "amount": {
                            "type": "number",
                            "description": "Amount contributed",
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Status of the contribution",
                            "enum": [
                              "PENDING",
                              "COMPLETED",
                              "CANCELLED",
                              "REJECTED"
                            ]
                          },
                          "createdAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Creation Date of the Contribution",
                            "nullable": false
                          },
                          "updatedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Last Update Date of the Contribution",
                            "nullable": true
                          },
                          "deletedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Deletion Date of the Contribution",
                            "nullable": true
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "ICO Contributions not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Creates a new ICO contribution",
        "description": "Allows a user to contribute to an ICO phase.",
        "operationId": "createIcoContribution",
        "tags": [
          "ICO",
          "Contributions"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "phaseId": {
                    "type": "string",
                    "description": "Phase ID for contribution"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount to contribute"
                  }
                },
                "required": [
                  "phaseId",
                  "amount"
                ]
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Contribution created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Contribution ID"
                    },
                    "amount": {
                      "type": "number",
                      "description": "Amount contributed"
                    },
                    "status": {
                      "type": "string",
                      "description": "Contribution status"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ico Contribution not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/ext/ico/offer/{id}": {
      "get": {
        "summary": "Retrieves a specific ICO token",
        "description": "Fetches details of a specific ICO token by ID, including phase and contribution details.",
        "operationId": "getIcoToken",
        "tags": [
          "ICO",
          "Tokens"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "Project ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "ICO token retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ICO token ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Token name",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Token status",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "phases": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Phase ID",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "phaseName": {
                            "type": "string",
                            "description": "Phase name",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Phase status",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "contributionPercentage": {
                            "type": "number",
                            "description": "Contribution percentage",
                            "nullable": false
                          },
                          "contributionsCount": {
                            "type": "integer",
                            "description": "Total contributions count",
                            "nullable": false
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ico Token not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ico/project/{id}": {
      "get": {
        "summary": "Retrieves a specific ICO project",
        "description": "Fetches details of a specific ICO project by ID.",
        "operationId": "getIcoProject",
        "tags": [
          "ICO",
          "Projects"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "description": "ICO project ID"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "ICO project retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ICO project ID",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Project name",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "description": {
                      "type": "string",
                      "description": "Project description",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Project status",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ico Project not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/ext/ico/project": {
      "get": {
        "summary": "Retrieves all ICO projects",
        "description": "Fetches a list of all ICO projects available.",
        "operationId": "listIcoProjects",
        "tags": [
          "ICO",
          "Projects"
        ],
        "responses": {
          "200": {
            "description": "ICO projects retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "ICO project ID",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Project name",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "description": {
                        "type": "string",
                        "description": "Project description",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "status": {
                        "type": "string",
                        "description": "Project status",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Ico Project not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/finance/currency/{type}/{code}/{method}": {
      "get": {
        "summary": "Retrieves a single currency by its ID",
        "description": "This endpoint retrieves a single currency by its ID.",
        "operationId": "getCurrencyById",
        "tags": [
          "Finance",
          "Currency"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "type",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "SPOT"
              ]
            }
          },
          {
            "index": 1,
            "name": "code",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 2,
            "name": "method",
            "in": "path",
            "required": false,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Currency retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "nullable": false
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "number",
                          "description": "ID of the currency",
                          "nullable": false
                        },
                        "name": {
                          "type": "string",
                          "description": "Currency name",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "symbol": {
                          "type": "string",
                          "description": "Currency symbol",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "precision": {
                          "type": "number",
                          "description": "Currency precision",
                          "nullable": false
                        },
                        "price": {
                          "type": "number",
                          "description": "Currency price",
                          "nullable": false
                        },
                        "status": {
                          "type": "boolean",
                          "description": "Currency status"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/currency/{type}/{code}": {
      "get": {
        "summary": "Retrieves a single currency by its ID",
        "description": "This endpoint retrieves a single currency by its ID.",
        "operationId": "getCurrencyById",
        "tags": [
          "Finance",
          "Currency"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "name": "action",
            "in": "query",
            "description": "The action to perform",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 0,
            "name": "type",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "FIAT",
                "SPOT",
                "ECO"
              ]
            }
          },
          {
            "index": 1,
            "name": "code",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Currency retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "nullable": false
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "number",
                          "description": "ID of the currency",
                          "nullable": false
                        },
                        "name": {
                          "type": "string",
                          "description": "Currency name",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "symbol": {
                          "type": "string",
                          "description": "Currency symbol",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "precision": {
                          "type": "number",
                          "description": "Currency precision",
                          "nullable": false
                        },
                        "price": {
                          "type": "number",
                          "description": "Currency price",
                          "nullable": false
                        },
                        "status": {
                          "type": "boolean",
                          "description": "Currency status"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/currency": {
      "get": {
        "summary": "Lists all currencies with their current rates",
        "description": "This endpoint retrieves all available currencies along with their current rates.",
        "operationId": "getCurrencies",
        "tags": [
          "Finance",
          "Currency"
        ],
        "parameters": [
          {
            "name": "action",
            "in": "query",
            "description": "The action to perform",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "walletType",
            "in": "query",
            "description": "The type of wallet to retrieve currencies for",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "targetWalletType",
            "in": "query",
            "description": "The type of wallet to transfer to",
            "required": false,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "Currencies retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "nullable": false
                    },
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "number",
                            "description": "ID of the currency",
                            "nullable": false
                          },
                          "name": {
                            "type": "string",
                            "description": "Currency name",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "symbol": {
                            "type": "string",
                            "description": "Currency symbol",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "precision": {
                            "type": "number",
                            "description": "Currency precision",
                            "nullable": false
                          },
                          "price": {
                            "type": "number",
                            "description": "Currency price",
                            "nullable": false
                          },
                          "status": {
                            "type": "boolean",
                            "description": "Currency status"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/currency/rate": {
      "get": {
        "summary": "Get exchange rate between two currencies",
        "description": "Returns the exchange rate between two currencies given their wallet types.",
        "operationId": "getExchangeRate",
        "tags": [
          "Finance",
          "Currency"
        ],
        "parameters": [
          {
            "name": "fromCurrency",
            "in": "query",
            "description": "The currency to convert from",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "fromType",
            "in": "query",
            "description": "The wallet type of the currency to convert from",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "toCurrency",
            "in": "query",
            "description": "The currency to convert to",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "toType",
            "in": "query",
            "description": "The wallet type of the currency to convert to",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "Exchange rate retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "nullable": false
                    },
                    "data": {
                      "type": "number",
                      "description": "Exchange rate from fromCurrency to toCurrency"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/currency/valid": {
      "get": {
        "summary": "Lists all currencies with their current rates",
        "description": "This endpoint retrieves all available currencies along with their current rates.",
        "operationId": "getCurrencies",
        "tags": [
          "Finance",
          "Currency"
        ],
        "parameters": [],
        "responses": {
          "200": {
            "description": "Currencies retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "nullable": false
                    },
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "number",
                            "description": "ID of the currency",
                            "nullable": false
                          },
                          "name": {
                            "type": "string",
                            "description": "Currency name",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "symbol": {
                            "type": "string",
                            "description": "Currency symbol",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "precision": {
                            "type": "number",
                            "description": "Currency precision",
                            "nullable": false
                          },
                          "price": {
                            "type": "number",
                            "description": "Currency price",
                            "nullable": false
                          },
                          "status": {
                            "type": "boolean",
                            "description": "Currency status"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Currency not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/finance/deposit/fiat": {
      "post": {
        "summary": "Performs a custom fiat deposit transaction",
        "description": "Initiates a custom fiat deposit transaction for the currently authenticated user",
        "operationId": "createCustomFiatDeposit",
        "tags": [
          "Wallets"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "methodId": {
                    "type": "string",
                    "description": "Deposit method ID"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount to deposit"
                  },
                  "currency": {
                    "type": "string",
                    "description": "Currency to deposit"
                  },
                  "customFields": {
                    "type": "object",
                    "description": "Custom data for the deposit"
                  }
                },
                "required": [
                  "methodId",
                  "amount",
                  "currency",
                  "customFields"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Custom deposit transaction initiated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Deposit Method not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/fiat/paypal/details": {
      "get": {
        "summary": "Fetches PayPal order details",
        "description": "Retrieves details for a specific PayPal order by its ID.",
        "operationId": "getPayPalOrderDetails",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "parameters": [
          {
            "name": "orderId",
            "in": "query",
            "description": "PayPal order ID",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "PayPal order details fetched successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Order ID"
                    },
                    "status": {
                      "type": "string",
                      "description": "Order status"
                    },
                    "purchase_units": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "amount": {
                            "type": "object",
                            "properties": {
                              "currency_code": {
                                "type": "string"
                              },
                              "value": {
                                "type": "string"
                              }
                            }
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Paypal not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/fiat/paypal": {
      "post": {
        "summary": "Creates a PayPal payment",
        "description": "Initiates a PayPal payment process by creating a new order.",
        "operationId": "createPayPalPayment",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "requestBody": {
          "description": "Payment information and application type",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "amount": {
                    "type": "number",
                    "description": "Payment amount in smallest currency unit (e.g., cents)"
                  },
                  "currency": {
                    "type": "string",
                    "description": "Currency code (e.g., USD)"
                  }
                },
                "required": [
                  "amount",
                  "currency"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "PayPal Order created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/fiat/paypal/verify": {
      "post": {
        "summary": "Verifies a Stripe checkout session",
        "description": "Confirms the validity of a Stripe checkout session by its session ID, ensuring the session is authenticated and retrieving associated payment intent and line items details.",
        "operationId": "verifyStripeCheckoutSession",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "name": "orderId",
            "in": "query",
            "description": "The PayPal order ID",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Checkout session verified successfully. Returns the session ID, payment intent status, and detailed line items.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "string",
                          "description": "Session ID"
                        },
                        "status": {
                          "type": "string",
                          "description": "Payment intent status",
                          "nullable": true
                        },
                        "lineItems": {
                          "type": "array",
                          "items": {
                            "type": "object",
                            "properties": {
                              "id": {
                                "type": "string",
                                "description": "Line item ID"
                              },
                              "description": {
                                "type": "string",
                                "description": "Line item description"
                              },
                              "amountSubtotal": {
                                "type": "number",
                                "description": "Subtotal amount"
                              },
                              "amountTotal": {
                                "type": "number",
                                "description": "Total amount"
                              },
                              "currency": {
                                "type": "string",
                                "description": "Currency code"
                              }
                            }
                          },
                          "description": "List of line items associated with the checkout session"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Paypal not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/fiat/stripe": {
      "post": {
        "summary": "Creates a Stripe payment intent or checkout session",
        "description": "Initiates a Stripe payment process by creating either a payment intent or a checkout session, based on the request parameters. This endpoint supports different workflows for web and Flutter applications.",
        "operationId": "createStripePayment",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "requestBody": {
          "description": "Payment information and application type",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "amount": {
                    "type": "number",
                    "description": "Payment amount in smallest currency unit (e.g., cents)"
                  },
                  "currency": {
                    "type": "string",
                    "description": "Currency code (e.g., USD)"
                  },
                  "intent": {
                    "type": "boolean",
                    "description": "Flag indicating if the request is from a mobile app",
                    "nullable": true
                  }
                },
                "required": [
                  "amount",
                  "currency"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Payment intent or checkout session created successfully. The response structure varies based on the request context: for Flutter applications, `id` and `clientSecret` are returned; for web applications, `version`, `id`, and `url` are provided.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Payment intent or session ID"
                    },
                    "clientSecret": {
                      "type": "string",
                      "description": "Client secret for payment intent",
                      "nullable": true
                    },
                    "version": {
                      "type": "string",
                      "description": "Stripe API version",
                      "nullable": true
                    },
                    "url": {
                      "type": "string",
                      "description": "Checkout session URL",
                      "nullable": true
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Stripe not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/fiat/stripe/verified": {
      "post": {
        "summary": "Verifies a Stripe checkout session",
        "description": "Confirms the validity of a Stripe checkout session by its session ID, ensuring the session is authenticated and retrieving associated payment intent and line items details.",
        "operationId": "verifyStripeCheckoutSession",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "sessionId",
            "in": "query",
            "description": "Stripe checkout session ID",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Checkout session verified successfully. Returns the session ID, payment intent status, and detailed line items.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Session ID"
                    },
                    "status": {
                      "type": "string",
                      "description": "Payment intent status",
                      "nullable": true
                    },
                    "lineItems": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Line item ID"
                          },
                          "description": {
                            "type": "string",
                            "description": "Line item description"
                          },
                          "amountSubtotal": {
                            "type": "number",
                            "description": "Subtotal amount"
                          },
                          "amountTotal": {
                            "type": "number",
                            "description": "Total amount"
                          },
                          "currency": {
                            "type": "string",
                            "description": "Currency code"
                          }
                        }
                      },
                      "description": "List of line items associated with the checkout session"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Stripe not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/fiat/stripe/verify": {
      "post": {
        "summary": "Verifies a Stripe checkout session",
        "description": "Confirms the validity of a Stripe checkout session by its session ID, ensuring the session is authenticated and retrieving associated payment intent and line items details.",
        "operationId": "verifyStripeCheckoutSession",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "sessionId",
            "in": "query",
            "description": "Stripe checkout session ID",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Checkout session verified successfully. Returns the session ID, payment intent status, and detailed line items.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "Session ID"
                    },
                    "status": {
                      "type": "string",
                      "description": "Payment intent status",
                      "nullable": true
                    },
                    "lineItems": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Line item ID"
                          },
                          "description": {
                            "type": "string",
                            "description": "Line item description"
                          },
                          "amountSubtotal": {
                            "type": "number",
                            "description": "Subtotal amount"
                          },
                          "amountTotal": {
                            "type": "number",
                            "description": "Total amount"
                          },
                          "currency": {
                            "type": "string",
                            "description": "Currency code"
                          }
                        }
                      },
                      "description": "List of line items associated with the checkout session"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Stripe not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/deposit/spot": {
      "post": {
        "summary": "Initiates a spot deposit transaction",
        "description": "This endpoint initiates a spot deposit transaction for the user",
        "operationId": "initiateSpotDeposit",
        "tags": [
          "Finance",
          "Deposit"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "currency": {
                    "type": "string"
                  },
                  "chain": {
                    "type": "string"
                  },
                  "trx": {
                    "type": "string"
                  }
                },
                "required": [
                  "currency",
                  "chain",
                  "trx"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Spot deposit transaction initiated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Deposit Method not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/investment/{id}": {
      "del": {
        "summary": "Cancels an investment",
        "description": "Allows a user to cancel an existing investment by its UUID. The operation reverses any financial transactions associated with the investment and updates the user’s wallet balance accordingly.",
        "operationId": "cancelInvestment",
        "tags": [
          "Finance",
          "Investment"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the investment to cancel",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "type",
            "in": "query",
            "description": "The type of investment to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Investment canceled successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Investment not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "Retrieves a single investment by UUID",
        "description": "Fetches detailed information about a specific investment identified by its UUID, including associated plan and user details.",
        "operationId": "getInvestment",
        "tags": [
          "Finance",
          "Investment"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The Id of the investment to retrieve",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "type",
            "in": "query",
            "description": "The type of investment to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Investment retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the investment",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "amount": {
                      "type": "number",
                      "description": "Amount of the investment",
                      "nullable": false
                    },
                    "roi": {
                      "type": "number",
                      "description": "Return on investment (ROI) of the investment",
                      "nullable": false
                    },
                    "duration": {
                      "type": "integer",
                      "description": "Duration of the investment in days",
                      "nullable": false
                    },
                    "status": {
                      "type": "string",
                      "description": "Status of the investment",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "user": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "string",
                          "description": "ID of the user",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "firstName": {
                          "type": "string",
                          "description": "First name of the user",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "lastName": {
                          "type": "string",
                          "description": "Last name of the user",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "avatar": {
                          "type": "string",
                          "description": "Avatar of the user",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        }
                      }
                    },
                    "plan": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "string",
                          "description": "ID of the investment plan",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "name": {
                          "type": "string",
                          "description": "Name of the investment plan",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "title": {
                          "type": "string",
                          "description": "Title of the investment plan",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "image": {
                          "type": "string",
                          "description": "Image of the investment plan",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "description": {
                          "type": "string",
                          "description": "Description of the investment plan",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "currency": {
                          "type": "string",
                          "description": "Currency of the investment plan",
                          "maxLength": 255,
                          "minLength": 0,
                          "nullable": false
                        },
                        "minAmount": {
                          "type": "number",
                          "description": "Minimum amount required for the investment plan",
                          "nullable": false
                        },
                        "maxAmount": {
                          "type": "number",
                          "description": "Maximum amount allowed for the investment plan",
                          "nullable": false
                        },
                        "roi": {
                          "type": "number",
                          "description": "Return on investment (ROI) of the investment plan",
                          "nullable": false
                        },
                        "duration": {
                          "type": "integer",
                          "description": "Duration of the investment plan in days",
                          "nullable": false
                        },
                        "status": {
                          "type": "boolean",
                          "description": "Status of the investment plan"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Investment not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/investment/analysis": {
      "post": {
        "summary": "Gets chart data for analytics",
        "operationId": "getAnalyticsData",
        "tags": [
          "Finance",
          "Investment"
        ],
        "parameters": [
          {
            "name": "model",
            "in": "query",
            "description": "Model to get data from",
            "schema": {
              "type": "string"
            },
            "required": true
          },
          {
            "name": "timeframe",
            "in": "query",
            "description": "Timeframe for the data",
            "schema": {
              "type": "string",
              "enum": [
                "h",
                "d",
                "w",
                "m",
                "3m",
                "6m",
                "y"
              ],
              "default": "m"
            }
          },
          {
            "name": "filter",
            "in": "query",
            "description": "Filter for the data",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "type",
            "in": "query",
            "description": "The type of investment to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "availableFilters": {
                    "type": "object",
                    "additionalProperties": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "value": {
                            "type": "string"
                          },
                          "label": {
                            "type": "string"
                          },
                          "color": {
                            "type": "string"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Analytics data of user counts per day",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "chartData": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "date": {
                            "type": "string"
                          },
                          "count": {
                            "type": "number"
                          }
                        }
                      }
                    },
                    "filterResults": {
                      "type": "object",
                      "additionalProperties": {
                        "type": "object",
                        "properties": {
                          "count": {
                            "type": "number"
                          },
                          "change": {
                            "type": "number"
                          },
                          "percentage": {
                            "type": "number"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized access"
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/investment": {
      "get": {
        "summary": "Lists all investments",
        "description": "Fetches a comprehensive list of all investments made by users, including details of the investment plan and user information.",
        "operationId": "listAllInvestments",
        "tags": [
          "Finance",
          "Investment"
        ],
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "type",
            "in": "query",
            "description": "The type of investment to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Investments retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the investment",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "amount": {
                            "type": "number",
                            "description": "Amount of the investment",
                            "nullable": false
                          },
                          "roi": {
                            "type": "number",
                            "description": "Return on investment (ROI) of the investment",
                            "nullable": false
                          },
                          "duration": {
                            "type": "integer",
                            "description": "Duration of the investment in days",
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Status of the investment",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "user": {
                            "type": "object",
                            "properties": {
                              "id": {
                                "type": "string",
                                "description": "ID of the user",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "firstName": {
                                "type": "string",
                                "description": "First name of the user",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "lastName": {
                                "type": "string",
                                "description": "Last name of the user",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "avatar": {
                                "type": "string",
                                "description": "Avatar of the user",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              }
                            }
                          },
                          "plan": {
                            "type": "object",
                            "properties": {
                              "id": {
                                "type": "string",
                                "description": "ID of the investment plan",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "name": {
                                "type": "string",
                                "description": "Name of the investment plan",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "title": {
                                "type": "string",
                                "description": "Title of the investment plan",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "image": {
                                "type": "string",
                                "description": "Image of the investment plan",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "description": {
                                "type": "string",
                                "description": "Description of the investment plan",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "currency": {
                                "type": "string",
                                "description": "Currency of the investment plan",
                                "maxLength": 255,
                                "minLength": 0,
                                "nullable": false
                              },
                              "minAmount": {
                                "type": "number",
                                "description": "Minimum amount required for the investment plan",
                                "nullable": false
                              },
                              "maxAmount": {
                                "type": "number",
                                "description": "Maximum amount allowed for the investment plan",
                                "nullable": false
                              },
                              "roi": {
                                "type": "number",
                                "description": "Return on investment (ROI) of the investment plan",
                                "nullable": false
                              },
                              "duration": {
                                "type": "integer",
                                "description": "Duration of the investment plan in days",
                                "nullable": false
                              },
                              "status": {
                                "type": "boolean",
                                "description": "Status of the investment plan"
                              }
                            }
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Investment not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Creates a new investment",
        "description": "Initiates a new investment based on the specified plan and amount. This process involves updating the user's wallet balance and creating transaction records.",
        "operationId": "createInvestment",
        "tags": [
          "Finance",
          "Investment"
        ],
        "parameters": [],
        "requestBody": {
          "description": "Data required to create a new investment",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "type": {
                    "type": "string",
                    "description": "The type of investment plan",
                    "example": "general"
                  },
                  "planId": {
                    "type": "string",
                    "description": "The unique identifier of the investment plan",
                    "example": "1"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Investment amount",
                    "example": 1000
                  },
                  "durationId": {
                    "type": "string",
                    "description": "The unique identifier of the investment duration",
                    "example": "1"
                  }
                },
                "required": [
                  "type",
                  "planId",
                  "durationId",
                  "amount"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Investment created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/investment/plan/{id}": {
      "get": {
        "summary": "Retrieves a single investment plan by ID",
        "description": "Fetches detailed information about a specific investment plan based on its unique identifier.",
        "operationId": "getInvestmentPlan",
        "tags": [
          "Finance",
          "Investment"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The ID of the investment plan to retrieve",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Investment plan retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the investment plan",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "name": {
                      "type": "string",
                      "description": "Name of the investment plan",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "title": {
                      "type": "string",
                      "description": "Title of the investment plan",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "image": {
                      "type": "string",
                      "description": "Image of the investment plan",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "description": {
                      "type": "string",
                      "description": "Description of the investment plan",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "currency": {
                      "type": "string",
                      "description": "Currency of the investment plan",
                      "maxLength": 255,
                      "minLength": 0,
                      "nullable": false
                    },
                    "minAmount": {
                      "type": "number",
                      "description": "Minimum amount required for the investment plan",
                      "nullable": false
                    },
                    "maxAmount": {
                      "type": "number",
                      "description": "Maximum amount allowed for the investment plan",
                      "nullable": false
                    },
                    "roi": {
                      "type": "number",
                      "description": "Return on investment (ROI) of the investment plan",
                      "nullable": false
                    },
                    "duration": {
                      "type": "integer",
                      "description": "Duration of the investment plan in days",
                      "nullable": false
                    },
                    "status": {
                      "type": "boolean",
                      "description": "Status of the investment plan"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Investment Plan not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": false,
        "security": []
      }
    },
    "/api/finance/investment/plan": {
      "get": {
        "summary": "Lists all investment plans",
        "description": "Retrieves a list of all available investment plans that are currently active and open for new investments.",
        "operationId": "listInvestmentPlans",
        "tags": [
          "Finance",
          "Investment"
        ],
        "responses": {
          "200": {
            "description": "Investment plans retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "ID of the investment plan",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "name": {
                        "type": "string",
                        "description": "Name of the investment plan",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "title": {
                        "type": "string",
                        "description": "Title of the investment plan",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "image": {
                        "type": "string",
                        "description": "Image of the investment plan",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "description": {
                        "type": "string",
                        "description": "Description of the investment plan",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "currency": {
                        "type": "string",
                        "description": "Currency of the investment plan",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "minAmount": {
                        "type": "number",
                        "description": "Minimum amount required for the investment plan",
                        "nullable": false
                      },
                      "maxAmount": {
                        "type": "number",
                        "description": "Maximum amount allowed for the investment plan",
                        "nullable": false
                      },
                      "roi": {
                        "type": "number",
                        "description": "Return on investment (ROI) of the investment plan",
                        "nullable": false
                      },
                      "duration": {
                        "type": "integer",
                        "description": "Duration of the investment plan in days",
                        "nullable": false
                      },
                      "status": {
                        "type": "boolean",
                        "description": "Status of the investment plan"
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Investment Plan not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": false,
        "security": []
      }
    },
    "/api/finance/investment/user": {
      "get": {
        "summary": "Retrieves investments for the logged-in user",
        "description": "Fetches all active investments associated with the currently authenticated user, including details about the investment plan and user information.",
        "operationId": "getUserInvestments",
        "tags": [
          "Finance",
          "Investment"
        ],
        "responses": {
          "200": {
            "description": "Investments retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string",
                        "description": "ID of the investment",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "amount": {
                        "type": "number",
                        "description": "Amount of the investment",
                        "nullable": false
                      },
                      "roi": {
                        "type": "number",
                        "description": "Return on investment (ROI) of the investment",
                        "nullable": false
                      },
                      "duration": {
                        "type": "integer",
                        "description": "Duration of the investment in days",
                        "nullable": false
                      },
                      "status": {
                        "type": "string",
                        "description": "Status of the investment",
                        "maxLength": 255,
                        "minLength": 0,
                        "nullable": false
                      },
                      "user": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "firstName": {
                            "type": "string",
                            "description": "First name of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "lastName": {
                            "type": "string",
                            "description": "Last name of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "avatar": {
                            "type": "string",
                            "description": "Avatar of the user",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          }
                        }
                      },
                      "plan": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the investment plan",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "name": {
                            "type": "string",
                            "description": "Name of the investment plan",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "title": {
                            "type": "string",
                            "description": "Title of the investment plan",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "image": {
                            "type": "string",
                            "description": "Image of the investment plan",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "description": {
                            "type": "string",
                            "description": "Description of the investment plan",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "currency": {
                            "type": "string",
                            "description": "Currency of the investment plan",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "minAmount": {
                            "type": "number",
                            "description": "Minimum amount required for the investment plan",
                            "nullable": false
                          },
                          "maxAmount": {
                            "type": "number",
                            "description": "Maximum amount allowed for the investment plan",
                            "nullable": false
                          },
                          "roi": {
                            "type": "number",
                            "description": "Return on investment (ROI) of the investment plan",
                            "nullable": false
                          },
                          "duration": {
                            "type": "integer",
                            "description": "Duration of the investment plan in days",
                            "nullable": false
                          },
                          "status": {
                            "type": "boolean",
                            "description": "Status of the investment plan"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Investment not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/transaction/{id}": {
      "get": {
        "summary": "Retrieves details of a specific transaction by reference ID",
        "description": "Fetches detailed information about a specific transaction based on its unique reference ID.",
        "operationId": "getTransaction",
        "tags": [
          "Finance",
          "Transactions"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The UUID of the transaction to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Transaction details retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the transaction"
                    },
                    "userId": {
                      "type": "string",
                      "description": "ID of the user who created the transaction"
                    },
                    "walletId": {
                      "type": "string",
                      "description": "ID of the wallet associated with the transaction"
                    },
                    "type": {
                      "type": "string",
                      "description": "Type of the transaction"
                    },
                    "status": {
                      "type": "string",
                      "description": "Status of the transaction"
                    },
                    "amount": {
                      "type": "number",
                      "description": "Amount of the transaction"
                    },
                    "fee": {
                      "type": "number",
                      "description": "Fee charged for the transaction"
                    },
                    "description": {
                      "type": "string",
                      "description": "Description of the transaction"
                    },
                    "metadata": {
                      "type": "object",
                      "description": "Metadata of the transaction"
                    },
                    "referenceId": {
                      "type": "string",
                      "description": "Reference ID of the transaction"
                    },
                    "createdAt": {
                      "type": "string",
                      "description": "Date and time when the transaction was created"
                    },
                    "updatedAt": {
                      "type": "string",
                      "description": "Date and time when the transaction was last updated"
                    },
                    "wallet": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "string",
                          "description": "ID of the wallet"
                        },
                        "userId": {
                          "type": "string",
                          "description": "ID of the user who owns the wallet"
                        },
                        "currency": {
                          "type": "string",
                          "description": "Currency of the wallet"
                        },
                        "type": {
                          "type": "string",
                          "description": "Type of the wallet"
                        },
                        "balance": {
                          "type": "number",
                          "description": "Current balance of the wallet"
                        },
                        "createdAt": {
                          "type": "string",
                          "description": "Date and time when the wallet was created"
                        },
                        "updatedAt": {
                          "type": "string",
                          "description": "Date and time when the wallet was last updated"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Transaction not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/transaction/analysis": {
      "post": {
        "summary": "Gets chart data for user analytics",
        "operationId": "getAnalyticsData",
        "tags": [
          "Finance",
          "Transactions"
        ],
        "parameters": [
          {
            "name": "timeframe",
            "in": "query",
            "description": "Timeframe for the data",
            "schema": {
              "type": "string",
              "enum": [
                "h",
                "d",
                "w",
                "m",
                "3m",
                "6m",
                "y"
              ],
              "default": "m"
            }
          },
          {
            "name": "filter",
            "in": "query",
            "description": "Filter for the data",
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "availableFilters": {
                    "type": "object",
                    "additionalProperties": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "value": {
                            "type": "string"
                          },
                          "label": {
                            "type": "string"
                          },
                          "color": {
                            "type": "string"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Analytics data of user counts per day",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "chartData": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "date": {
                            "type": "string"
                          },
                          "count": {
                            "type": "number"
                          }
                        }
                      }
                    },
                    "filterResults": {
                      "type": "object",
                      "additionalProperties": {
                        "type": "object",
                        "properties": {
                          "count": {
                            "type": "number"
                          },
                          "change": {
                            "type": "number"
                          },
                          "percentage": {
                            "type": "number"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized access"
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/transaction": {
      "get": {
        "summary": "Lists transactions with optional filters",
        "operationId": "listTransactions",
        "tags": [
          "Finance",
          "Transactions"
        ],
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "walletType",
            "in": "query",
            "description": "Type of the wallet",
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "currency",
            "in": "query",
            "description": "Currency of the wallet",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Paginated list of transactions retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the transaction",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": true
                          },
                          "type": {
                            "type": "string",
                            "description": "Type of the transaction (DEPOSIT, WITHDRAW, etc.)",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Current status of the transaction (PENDING, COMPLETED, etc.)",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false,
                            "enum": [
                              "PENDING",
                              "COMPLETED",
                              "FAILED",
                              "CANCELLED",
                              "REJECTED",
                              "EXPIRED"
                            ]
                          },
                          "amount": {
                            "type": "number",
                            "description": "Amount involved in the transaction",
                            "nullable": false
                          },
                          "fee": {
                            "type": "number",
                            "description": "Fee associated with the transaction",
                            "nullable": false
                          },
                          "description": {
                            "type": "string",
                            "description": "Description of the transaction",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "metadata": {
                            "type": "object",
                            "description": "Additional metadata of the transaction",
                            "nullable": true
                          },
                          "referenceId": {
                            "type": "string",
                            "description": "Reference ID of the transaction",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": true
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Transactions not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/transaction/structure": {
      "get": {
        "summary": "Get form structure for transactions",
        "operationId": "getTransactionsStructure",
        "tags": [
          "Finance",
          "Transactions"
        ],
        "responses": {
          "200": {
            "description": "Form structure for transactions",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "oneOf": [
                      {
                        "type": "object",
                        "properties": {
                          "type": {
                            "type": "string",
                            "enum": [
                              "input",
                              "select",
                              "switch",
                              "file"
                            ]
                          },
                          "label": {
                            "type": "string"
                          },
                          "name": {
                            "type": "string"
                          },
                          "placeholder": {
                            "type": "string",
                            "nullable": true
                          },
                          "options": {
                            "type": "array",
                            "items": {
                              "type": "string"
                            },
                            "nullable": true
                          },
                          "fileType": {
                            "type": "string",
                            "nullable": true
                          },
                          "width": {
                            "type": "integer",
                            "nullable": true
                          },
                          "height": {
                            "type": "integer",
                            "nullable": true
                          },
                          "maxSize": {
                            "type": "number",
                            "nullable": true
                          },
                          "notNull": {
                            "type": "boolean",
                            "nullable": true
                          },
                          "ts": {
                            "type": "string"
                          }
                        },
                        "required": [
                          "type",
                          "label",
                          "name"
                        ]
                      },
                      {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "type": {
                              "type": "string",
                              "enum": [
                                "input",
                                "select",
                                "switch",
                                "file"
                              ]
                            },
                            "label": {
                              "type": "string"
                            },
                            "name": {
                              "type": "string"
                            },
                            "placeholder": {
                              "type": "string",
                              "nullable": true
                            },
                            "options": {
                              "type": "array",
                              "items": {
                                "type": "string"
                              },
                              "nullable": true
                            },
                            "fileType": {
                              "type": "string",
                              "nullable": true
                            },
                            "width": {
                              "type": "integer",
                              "nullable": true
                            },
                            "height": {
                              "type": "integer",
                              "nullable": true
                            },
                            "maxSize": {
                              "type": "number",
                              "nullable": true
                            },
                            "notNull": {
                              "type": "boolean",
                              "nullable": true
                            },
                            "ts": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "type",
                            "label",
                            "name"
                          ]
                        }
                      }
                    ]
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/finance/transfer": {
      "post": {
        "summary": "Performs a transfer transaction",
        "description": "Initiates a transfer transaction for the currently authenticated user",
        "operationId": "createTransfer",
        "tags": [
          "Finance",
          "Transfer"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "fromType": {
                    "type": "string",
                    "description": "The type of wallet to transfer from"
                  },
                  "toType": {
                    "type": "string",
                    "description": "The type of wallet to transfer to"
                  },
                  "fromCurrency": {
                    "type": "string",
                    "description": "The currency to transfer from"
                  },
                  "toCurrency": {
                    "type": "string",
                    "description": "The currency to transfer to",
                    "nullable": true
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount to transfer"
                  },
                  "transferType": {
                    "type": "string",
                    "description": "Type of transfer: client or wallet"
                  },
                  "clientId": {
                    "type": "string",
                    "description": "Client UUID for client transfers",
                    "nullable": true
                  }
                },
                "required": [
                  "fromType",
                  "toType",
                  "amount",
                  "fromCurrency",
                  "transferType"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Transfer transaction initiated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Withdraw Method not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/wallet/{type}/{currency}": {
      "get": {
        "summary": "Retrieves details of a specific wallet",
        "description": "Fetches detailed information about a specific wallet based on its unique identifier.",
        "operationId": "getWallet",
        "tags": [
          "Finance",
          "Wallets"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "type",
            "in": "path",
            "required": true,
            "description": "The type of wallet to retrieve",
            "schema": {
              "type": "string"
            }
          },
          {
            "index": 1,
            "name": "currency",
            "in": "path",
            "required": true,
            "description": "The currency of the wallet to retrieve",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Wallet details retrieved successfully"
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/wallet": {
      "get": {
        "summary": "Lists all wallets with optional filters",
        "operationId": "listWallets",
        "tags": [
          "Finance",
          "Wallets"
        ],
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "pnl",
            "in": "query",
            "description": "Fetch PnL data for the last 28 days",
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "List of wallets with pagination metadata",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the wallet",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "type": {
                            "type": "string",
                            "description": "Type of the wallet",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "currency": {
                            "type": "string",
                            "description": "Currency of the wallet",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "balance": {
                            "type": "number",
                            "description": "Current balance of the wallet",
                            "nullable": false
                          },
                          "inOrder": {
                            "type": "number",
                            "description": "Amount currently held in orders",
                            "nullable": false
                          },
                          "status": {
                            "type": "boolean",
                            "description": "Status of the wallet (active or inactive)"
                          },
                          "user": {
                            "type": "object",
                            "properties": {
                              "id": {
                                "type": "string",
                                "description": "User ID"
                              },
                              "firstName": {
                                "type": "string",
                                "description": "First name of the user"
                              },
                              "lastName": {
                                "type": "string",
                                "description": "Last name of the user"
                              },
                              "avatar": {
                                "type": "string",
                                "description": "Avatar URL of the user"
                              }
                            }
                          },
                          "transactions": {
                            "type": "array",
                            "description": "List of transactions associated with the wallet",
                            "items": {
                              "type": "object",
                              "properties": {
                                "id": {
                                  "type": "string",
                                  "description": "Transaction ID"
                                },
                                "amount": {
                                  "type": "number",
                                  "description": "Amount of the transaction"
                                },
                                "fee": {
                                  "type": "number",
                                  "description": "Transaction fee"
                                },
                                "type": {
                                  "type": "string",
                                  "description": "Type of the transaction"
                                },
                                "status": {
                                  "type": "string",
                                  "description": "Status of the transaction"
                                },
                                "createdAt": {
                                  "type": "string",
                                  "format": "date-time",
                                  "description": "Creation date of the transaction"
                                },
                                "metadata": {
                                  "type": "object",
                                  "description": "Metadata of the transaction"
                                }
                              }
                            }
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallets not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/wallet/symbol": {
      "get": {
        "summary": "Retrieves details of a specific wallet",
        "description": "Fetches detailed information about a specific wallet based on its unique identifier.",
        "operationId": "getWallet",
        "tags": [
          "Finance",
          "Wallets"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "in": "query",
            "name": "type",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "ECO",
                "SPOT"
              ]
            },
            "description": "The type of wallet to retrieve"
          },
          {
            "in": "query",
            "name": "currency",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The currency of the wallet to retrieve"
          },
          {
            "in": "query",
            "name": "pair",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The pair of the wallet to retrieve"
          }
        ],
        "responses": {
          "200": {
            "description": "Wallet details retrieved successfully"
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Wallet not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/withdraw/fiat": {
      "post": {
        "summary": "Performs a custom fiat withdraw transaction",
        "description": "Initiates a custom fiat withdraw transaction for the currently authenticated user",
        "operationId": "createCustomFiatWithdraw",
        "tags": [
          "Wallets"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "methodId": {
                    "type": "string",
                    "description": "Withdraw method ID"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount to withdraw"
                  },
                  "currency": {
                    "type": "string",
                    "description": "Currency to withdraw"
                  },
                  "customFields": {
                    "type": "object",
                    "description": "Custom data for the withdraw"
                  }
                },
                "required": [
                  "methodId",
                  "amount",
                  "currency",
                  "customFields"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Custom withdraw transaction initiated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Withdraw Method not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/finance/withdraw/spot": {
      "post": {
        "summary": "Performs a withdraw transaction",
        "description": "Initiates a withdraw transaction for the currently authenticated user",
        "operationId": "createWithdraw",
        "tags": [
          "Wallets"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "currency": {
                    "type": "string",
                    "description": "Currency to withdraw"
                  },
                  "chain": {
                    "type": "string",
                    "description": "Withdraw method ID"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Amount to withdraw"
                  },
                  "toAddress": {
                    "type": "string",
                    "description": "Withdraw toAddress"
                  }
                },
                "required": [
                  "currency",
                  "chain",
                  "amount",
                  "toAddress"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Withdraw transaction initiated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Withdraw not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/locale/{lng}/{ns}": {
      "post": {
        "summary": "Adds missing translations for the specified language and namespace",
        "operationId": "addTranslations",
        "tags": [
          "Translations"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "lng",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "Language code"
          },
          {
            "index": 1,
            "name": "ns",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "Namespace"
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "additionalProperties": true
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Translations added successfully"
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": []
      }
    },
    "/api/settings": {
      "get": {
        "summary": "Retrieves the application settings",
        "description": "This endpoint retrieves the application settings.",
        "operationId": "getSettings",
        "tags": [
          "Settings"
        ],
        "requiresAuth": false,
        "responses": {
          "200": {
            "description": "Application settings retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "key": {
                        "type": "string",
                        "description": "Setting key"
                      },
                      "value": {
                        "type": "string",
                        "description": "Setting value"
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Settings not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/upload/heic": {
      "post": {
        "summary": "Converts a HEIC image to JPEG format",
        "description": "Converts a HEIC image to JPEG format and returns the file URL",
        "operationId": "convertHeicFile",
        "tags": [
          "Conversion"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "dir": {
                    "type": "string",
                    "description": "Directory to save the converted file"
                  },
                  "file": {
                    "type": "string",
                    "description": "Base64 encoded HEIC file data"
                  },
                  "mimeType": {
                    "type": "string",
                    "description": "MIME type of the file"
                  }
                },
                "required": [
                  "dir",
                  "file",
                  "mimeType"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "File converted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "url": {
                      "type": "string",
                      "description": "URL of the converted file"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Conversion not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/upload": {
      "post": {
        "summary": "Uploads a file to a specified directory",
        "description": "Uploads a file to a specified directory",
        "operationId": "uploadFile",
        "tags": [
          "Upload"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "dir": {
                    "type": "string",
                    "description": "Directory to upload file to"
                  },
                  "file": {
                    "type": "string",
                    "description": "Base64 encoded file data"
                  },
                  "height": {
                    "type": "number",
                    "description": "Height of the image"
                  },
                  "width": {
                    "type": "number",
                    "description": "Width of the image"
                  },
                  "oldPath": {
                    "type": "string",
                    "description": "Path of the old image to remove"
                  }
                },
                "required": [
                  "dir",
                  "file"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "File uploaded successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "url": {
                      "type": "string",
                      "description": "URL of the uploaded file"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Upload not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/kyc/application/{id}": {
      "put": {
        "summary": "Updates KYC data for a given ID",
        "description": "This endpoint allows for the updating of Know Your Customer (KYC) data associated with a specific record. It requires authentication and appropriate permissions to perform the update.",
        "operationId": "updateKYCData",
        "tags": [
          "KYC"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "The ID of the KYC record to update",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "description": "Data to update the KYC record with",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "fields": {
                    "type": "object",
                    "description": "Detailed data following the KYC template structure"
                  },
                  "level": {
                    "type": "number",
                    "description": "Verification level intended with this KYC submission"
                  }
                },
                "required": [
                  "fields",
                  "level"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "KYC updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "KYC not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/kyc/application": {
      "get": {
        "summary": "Retrieves KYC data for the logged-in user",
        "description": "Fetches the Know Your Customer (KYC) data for the currently authenticated user. This endpoint requires user authentication and returns the user’s KYC information, including the status of the KYC verification process.",
        "operationId": "getUserKycData",
        "tags": [
          "KYC"
        ],
        "responses": {
          "200": {
            "description": "KYC data retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "number",
                          "description": "KYC ID"
                        },
                        "userId": {
                          "type": "number",
                          "description": "User ID associated with the KYC record"
                        },
                        "templateId": {
                          "type": "number",
                          "description": "ID of the KYC template used"
                        },
                        "data": {
                          "type": "object",
                          "description": "KYC data as a JSON object",
                          "nullable": true
                        },
                        "status": {
                          "type": "string",
                          "description": "Current status of the KYC verification",
                          "enum": [
                            "PENDING",
                            "APPROVED",
                            "REJECTED"
                          ]
                        },
                        "level": {
                          "type": "number",
                          "description": "Verification level"
                        },
                        "notes": {
                          "type": "string",
                          "description": "Administrative notes, if any",
                          "nullable": true
                        },
                        "createdAt": {
                          "type": "string",
                          "format": "date-time",
                          "description": "Timestamp when the KYC record was created"
                        },
                        "updatedAt": {
                          "type": "string",
                          "format": "date-time",
                          "description": "Timestamp when the KYC record was last updated"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Kyc not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Submits KYC data for the user",
        "description": "Submits Know Your Customer (KYC) data for the currently authenticated user based on a specific KYC template and level of verification required. This submission will initiate or update the user’s KYC verification process.",
        "operationId": "submitUserKycData",
        "tags": [
          "KYC"
        ],
        "requestBody": {
          "description": "KYC data submission details",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "templateId": {
                    "type": "string",
                    "description": "ID of the KYC template to be used for submission"
                  },
                  "fields": {
                    "type": "object",
                    "description": "Detailed data following the KYC template structure"
                  },
                  "level": {
                    "type": "number",
                    "description": "Verification level intended with this KYC submission"
                  }
                },
                "required": [
                  "templateId",
                  "fields",
                  "level"
                ]
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "KYC data submitted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful submission of KYC data"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Kyc not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/kyc/template": {
      "get": {
        "summary": "Lists the active KYC template",
        "description": "Fetches the currently active KYC (Know Your Customer) template that is used for KYC processes. This endpoint is accessible without authentication and returns the template that is marked as active in the system.",
        "operationId": "getActiveKycTemplate",
        "tags": [
          "KYC"
        ],
        "responses": {
          "200": {
            "description": "Active KYC template retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "number",
                      "description": "Template ID"
                    },
                    "title": {
                      "type": "string",
                      "description": "Template title"
                    },
                    "options": {
                      "type": "object",
                      "description": "Template options as JSON object",
                      "nullable": true
                    },
                    "status": {
                      "type": "boolean",
                      "description": "Active status of the template"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Kyc Template not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": false,
        "security": []
      }
    },
    "/api/user/notification/{id}": {
      "del": {
        "summary": "Deletes a specific notification",
        "operationId": "deleteNotification",
        "tags": [
          "Notifications"
        ],
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "description": "ID of the notification to delete",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "restore",
            "in": "query",
            "description": "Restore the notification instead of deleting",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "force",
            "in": "query",
            "description": "Delete the notification permanently",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "notification deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message indicating successful deletion"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "notification not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/notification/clean": {
      "del": {
        "summary": "delete all notifications",
        "operationId": "bulkDeleteNotifications",
        "tags": [
          "Notifications"
        ],
        "parameters": [
          {
            "in": "query",
            "name": "type",
            "description": "Type of notification",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Notifications deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Notifications not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/notification": {
      "del": {
        "summary": "Bulk deletes notifications by IDs",
        "operationId": "bulkDeleteNotifications",
        "tags": [
          "Notifications"
        ],
        "parameters": [
          {
            "name": "restore",
            "in": "query",
            "description": "Restore the Notifications instead of deleting",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          },
          {
            "name": "force",
            "in": "query",
            "description": "Delete the Notifications permanently",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "ids": {
                    "type": "array",
                    "items": {
                      "type": "string"
                    },
                    "description": "Array of notification IDs to delete"
                  }
                },
                "required": [
                  "ids"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Notifications deleted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Notifications not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "get": {
        "summary": "List all notifications",
        "description": "Retrieves a paginated list of all notifications for users.",
        "operationId": "getNotifications",
        "tags": [
          "Notifications"
        ],
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Notifications retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "Notification ID"
                          },
                          "type": {
                            "type": "string",
                            "description": "Notification type"
                          },
                          "title": {
                            "type": "string",
                            "description": "Notification title"
                          },
                          "message": {
                            "type": "string",
                            "description": "Notification message"
                          },
                          "link": {
                            "type": "string",
                            "description": "Link associated with the notification"
                          },
                          "createdAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Creation date of the notification"
                          },
                          "updatedAt": {
                            "type": "string",
                            "format": "date-time",
                            "description": "Last update date of the notification"
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Notifications not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/notification/structure": {
      "get": {
        "summary": "Get form structure for Notifications",
        "operationId": "getNotificationsStructure",
        "tags": [
          "Notifications"
        ],
        "responses": {
          "200": {
            "description": "Form structure for Notifications",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "oneOf": [
                      {
                        "type": "object",
                        "properties": {
                          "type": {
                            "type": "string",
                            "enum": [
                              "input",
                              "select",
                              "switch",
                              "file"
                            ]
                          },
                          "label": {
                            "type": "string"
                          },
                          "name": {
                            "type": "string"
                          },
                          "placeholder": {
                            "type": "string",
                            "nullable": true
                          },
                          "options": {
                            "type": "array",
                            "items": {
                              "type": "string"
                            },
                            "nullable": true
                          },
                          "fileType": {
                            "type": "string",
                            "nullable": true
                          },
                          "width": {
                            "type": "integer",
                            "nullable": true
                          },
                          "height": {
                            "type": "integer",
                            "nullable": true
                          },
                          "maxSize": {
                            "type": "number",
                            "nullable": true
                          },
                          "notNull": {
                            "type": "boolean",
                            "nullable": true
                          },
                          "ts": {
                            "type": "string"
                          }
                        },
                        "required": [
                          "type",
                          "label",
                          "name"
                        ]
                      },
                      {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "type": {
                              "type": "string",
                              "enum": [
                                "input",
                                "select",
                                "switch",
                                "file"
                              ]
                            },
                            "label": {
                              "type": "string"
                            },
                            "name": {
                              "type": "string"
                            },
                            "placeholder": {
                              "type": "string",
                              "nullable": true
                            },
                            "options": {
                              "type": "array",
                              "items": {
                                "type": "string"
                              },
                              "nullable": true
                            },
                            "fileType": {
                              "type": "string",
                              "nullable": true
                            },
                            "width": {
                              "type": "integer",
                              "nullable": true
                            },
                            "height": {
                              "type": "integer",
                              "nullable": true
                            },
                            "maxSize": {
                              "type": "number",
                              "nullable": true
                            },
                            "notNull": {
                              "type": "boolean",
                              "nullable": true
                            },
                            "ts": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "type",
                            "label",
                            "name"
                          ]
                        }
                      }
                    ]
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    },
    "/api/user/profile": {
      "get": {
        "summary": "Retrieves the profile of the current user",
        "description": "Fetches the profile of the currently authenticated user",
        "operationId": "getProfile",
        "tags": [
          "Auth"
        ],
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "User profile retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {
                      "type": "string",
                      "description": "ID of the user"
                    },
                    "email": {
                      "type": "string",
                      "description": "Email of the user"
                    },
                    "firstName": {
                      "type": "string",
                      "description": "First name of the user"
                    },
                    "lastName": {
                      "type": "string",
                      "description": "Last name of the user"
                    },
                    "role": {
                      "type": "string",
                      "description": "Role of the user"
                    },
                    "createdAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Date and time when the user was created"
                    },
                    "updatedAt": {
                      "type": "string",
                      "format": "date-time",
                      "description": "Date and time when the user was last updated"
                    }
                  },
                  "required": [
                    "id",
                    "email",
                    "firstName",
                    "lastName",
                    "role",
                    "createdAt",
                    "updatedAt"
                  ]
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "User not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "put": {
        "summary": "Updates the profile of the current user",
        "description": "Updates the profile of the currently authenticated user",
        "operationId": "updateProfile",
        "tags": [
          "Auth"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "firstName": {
                    "type": "string",
                    "description": "First name of the user"
                  },
                  "lastName": {
                    "type": "string",
                    "description": "Last name of the user"
                  },
                  "email": {
                    "type": "string",
                    "format": "email",
                    "description": "Email of the user"
                  },
                  "metadata": {
                    "type": "object",
                    "description": "Metadata of the user"
                  },
                  "avatar": {
                    "type": "string",
                    "description": "Avatar of the user",
                    "nullable": true
                  },
                  "phone": {
                    "type": "string",
                    "description": "Phone number of the user"
                  },
                  "emailVerified": {
                    "type": "boolean",
                    "description": "Email verification status"
                  },
                  "twoFactor": {
                    "type": "boolean",
                    "description": "Two-factor authentication status"
                  },
                  "profile": {
                    "type": "object",
                    "properties": {
                      "bio": {
                        "type": "string",
                        "description": "User bio"
                      },
                      "location": {
                        "type": "object",
                        "properties": {
                          "address": {
                            "type": "string",
                            "description": "User address"
                          },
                          "city": {
                            "type": "string",
                            "description": "User city"
                          },
                          "country": {
                            "type": "string",
                            "description": "User country"
                          },
                          "zip": {
                            "type": "string",
                            "description": "User zip code"
                          }
                        }
                      },
                      "social": {
                        "type": "object",
                        "properties": {
                          "twitter": {
                            "type": "string",
                            "description": "Twitter profile"
                          },
                          "dribbble": {
                            "type": "string",
                            "description": "Dribbble profile"
                          },
                          "instagram": {
                            "type": "string",
                            "description": "Instagram profile"
                          },
                          "github": {
                            "type": "string",
                            "description": "GitHub profile"
                          },
                          "gitlab": {
                            "type": "string",
                            "description": "GitLab profile"
                          },
                          "telegram": {
                            "type": "string",
                            "description": "Telegram username"
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "User profile updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "User not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/profile/otp": {
      "post": {
        "summary": "Saves the OTP configuration for the user",
        "operationId": "saveOTP",
        "description": "Saves the OTP configuration for the user",
        "tags": [
          "Profile"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "secret": {
                    "type": "string",
                    "description": "OTP secret"
                  },
                  "type": {
                    "type": "string",
                    "description": "Type of OTP",
                    "enum": [
                      "SMS",
                      "APP"
                    ]
                  }
                },
                "required": [
                  "secret",
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP configuration saved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "message": {
                          "type": "string",
                          "description": "Success message"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "User not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/profile/otp/secret": {
      "post": {
        "summary": "Generates an OTP secret and sends OTP via SMS or generates a QR code for OTP APP",
        "description": "Generates an OTP secret and sends OTP via SMS or generates a QR code for OTP APP",
        "operationId": "generateOTPSecret",
        "tags": [
          "Profile"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "type": {
                    "type": "string",
                    "description": "Type of OTP to generate",
                    "enum": [
                      "SMS",
                      "APP"
                    ]
                  },
                  "phoneNumber": {
                    "type": "string",
                    "description": "Phone number to send the OTP to"
                  },
                  "email": {
                    "type": "string",
                    "description": "Email to generate the QR code for OTP APP"
                  }
                },
                "required": [
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP secret generated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "secret": {
                          "type": "string",
                          "description": "OTP secret"
                        },
                        "qrCode": {
                          "type": "string",
                          "description": "QR code for OTP APP"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "User not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/profile/otp/status": {
      "post": {
        "summary": "Toggles the OTP feature for the user account",
        "operationId": "toggleOTP",
        "description": "Toggles the OTP feature for the user account",
        "tags": [
          "Profile"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "status": {
                    "type": "boolean",
                    "description": "Status of the OTP feature"
                  }
                },
                "required": [
                  "status"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP feature toggled successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "message": {
                          "type": "string",
                          "description": "Message indicating the status of the OTP feature"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "User not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/profile/otp/verify": {
      "post": {
        "summary": "Verifies an OTP with the provided secret and type, and saves it if valid",
        "operationId": "verifyOTP",
        "description": "Verifies an OTP with the provided secret and type, and saves it if valid",
        "tags": [
          "Profile"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "otp": {
                    "type": "string",
                    "description": "OTP to verify"
                  },
                  "secret": {
                    "type": "string",
                    "description": "OTP secret"
                  },
                  "type": {
                    "type": "string",
                    "description": "Type of OTP",
                    "enum": [
                      "SMS",
                      "APP"
                    ]
                  }
                },
                "required": [
                  "otp",
                  "secret",
                  "type"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "OTP verified and saved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "message": {
                          "type": "string",
                          "description": "Message indicating the status of the OTP verification"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "User not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/profile/wallet/connect": {
      "post": {
        "summary": "Registers a wallet address for the user",
        "description": "Registers a wallet address for the authenticated user",
        "operationId": "registerWallet",
        "tags": [
          "Auth"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "address": {
                    "type": "string",
                    "description": "Wallet address"
                  },
                  "chainId": {
                    "type": "number",
                    "description": "Blockchain chain ID"
                  }
                },
                "required": [
                  "address",
                  "chainId"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Wallet address registered successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing address or chainId)"
          },
          "401": {
            "description": "Unauthorized (e.g., user not authenticated)"
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/profile/wallet/disconnect": {
      "post": {
        "summary": "Disconnects a wallet address for the user",
        "description": "Disconnects a wallet address for the authenticated user and removes the record from providerUser",
        "operationId": "disconnectWallet",
        "tags": [
          "Auth"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "address": {
                    "type": "string",
                    "description": "Wallet address"
                  }
                },
                "required": [
                  "address"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Wallet address disconnected successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Success message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request (e.g., missing address)"
          },
          "401": {
            "description": "Unauthorized (e.g., user not authenticated)"
          },
          "500": {
            "description": "Internal server error"
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/support/chat": {
      "get": {
        "summary": "Retrieves or creates a live chat ticket",
        "description": "Fetches the existing live chat ticket for the authenticated user, or creates a new one if none exists.",
        "operationId": "getOrCreateLiveChat",
        "tags": [
          "Support"
        ],
        "requiresAuth": true,
        "responses": {
          "200": {
            "description": "Support Ticket created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/support/ticket/{id}/close": {
      "put": {
        "summary": "Closes a support ticket",
        "description": "Closes a support ticket identified by its UUID.",
        "operationId": "closeTicket",
        "tags": [
          "Support"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The UUID of the ticket to close",
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Support Ticket updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Support Ticket not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/support/ticket/{id}": {
      "get": {
        "summary": "Retrieves a single ticket details for the logged-in user",
        "description": "Fetches detailed information about a specific support ticket identified by its ID, including associated chat details.",
        "operationId": "getTicket",
        "tags": [
          "Support"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The ID of the ticket to retrieve",
            "schema": {
              "type": "number"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Ticket details retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "status": {
                      "type": "boolean",
                      "description": "Indicates if the request was successful"
                    },
                    "statusCode": {
                      "type": "number",
                      "description": "HTTP status code",
                      "example": 200
                    },
                    "data": {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "string",
                          "description": "ID of the ticket"
                        },
                        "userId": {
                          "type": "string",
                          "description": "ID of the user who created the ticket"
                        },
                        "agentId": {
                          "type": "string",
                          "description": "ID of the agent assigned to the ticket"
                        },
                        "subject": {
                          "type": "string",
                          "description": "Subject of the ticket"
                        },
                        "importance": {
                          "type": "string",
                          "description": "Importance level of the ticket"
                        },
                        "status": {
                          "type": "string",
                          "description": "Status of the ticket"
                        },
                        "messages": {
                          "type": "object",
                          "description": "Messages associated with the chat"
                        },
                        "createdAt": {
                          "type": "string",
                          "format": "date-time",
                          "description": "Date and time the ticket was created"
                        },
                        "updatedAt": {
                          "type": "string",
                          "format": "date-time",
                          "description": "Date and time the ticket was updated"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Support Ticket not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Reply to a support ticket",
        "description": "Reply to a support ticket identified by its UUID.",
        "operationId": "replyTicket",
        "tags": [
          "Support"
        ],
        "requiresAuth": true,
        "parameters": [
          {
            "index": 0,
            "name": "id",
            "in": "path",
            "required": true,
            "description": "The UUID of the ticket to reply to",
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "description": "The message to send",
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "type": {
                    "type": "string",
                    "enum": [
                      "client",
                      "agent"
                    ]
                  },
                  "time": {
                    "type": "string",
                    "format": "date-time"
                  },
                  "userId": {
                    "type": "string"
                  },
                  "content": {
                    "type": "string"
                  },
                  "attachment": {
                    "type": "string"
                  }
                },
                "required": [
                  "type",
                  "time",
                  "userId"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Support Ticket updated successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Support Ticket not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/support/ticket": {
      "get": {
        "summary": "Lists all tickets for the logged-in user",
        "operationId": "listTickets",
        "tags": [
          "Support"
        ],
        "description": "Fetches all support tickets associated with the currently authenticated user.",
        "parameters": [
          {
            "name": "filter",
            "in": "query",
            "description": "Filter criteria for records.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "perPage",
            "in": "query",
            "description": "Number of records per page. Default: 10.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "page",
            "in": "query",
            "description": "Page number. Default: 1.",
            "required": false,
            "schema": {
              "type": "number"
            }
          },
          {
            "name": "sortField",
            "in": "query",
            "description": "Field name to sort by.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "sortOrder",
            "in": "query",
            "description": "Order of sorting: asc or desc.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "asc",
                "desc"
              ]
            }
          },
          {
            "name": "showDeleted",
            "in": "query",
            "description": "Show deleted records. Default: false.",
            "required": false,
            "schema": {
              "type": "boolean"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Posts retrieved successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "data": {
                      "type": "array",
                      "items": {
                        "type": "object",
                        "properties": {
                          "id": {
                            "type": "string",
                            "description": "ID of the support ticket",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": true
                          },
                          "userId": {
                            "type": "string",
                            "description": "ID of the user who created the ticket",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "agentId": {
                            "type": "string",
                            "description": "ID of the agent assigned to the ticket",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "messages": {
                            "type": "object",
                            "description": "Messages associated with the chat"
                          },
                          "subject": {
                            "type": "string",
                            "description": "Subject of the ticket",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "importance": {
                            "type": "string",
                            "description": "Importance of the ticket",
                            "maxLength": 255,
                            "minLength": 0,
                            "nullable": false
                          },
                          "status": {
                            "type": "string",
                            "description": "Status of the ticket",
                            "enum": [
                              "PENDING",
                              "OPEN",
                              "REPLIED",
                              "CLOSED"
                            ]
                          },
                          "type": {
                            "type": "string",
                            "description": "Type of the ticket",
                            "enum": [
                              "LIVE",
                              "TICKET"
                            ]
                          }
                        }
                      }
                    },
                    "pagination": {
                      "type": "object",
                      "properties": {
                        "totalItems": {
                          "type": "integer",
                          "description": "Total number of users"
                        },
                        "currentPage": {
                          "type": "integer",
                          "description": "Current page number"
                        },
                        "perPage": {
                          "type": "integer",
                          "description": "Number of users per page"
                        },
                        "totalPages": {
                          "type": "integer",
                          "description": "Total number of pages"
                        }
                      }
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "404": {
            "description": "Support Ticket not found",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "requiresAuth": true,
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      },
      "post": {
        "summary": "Creates a new support ticket",
        "description": "Creates a new support ticket for the currently authenticated user",
        "operationId": "createTicket",
        "tags": [
          "Support"
        ],
        "requiresAuth": true,
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "subject": {
                    "type": "string",
                    "description": "Subject of the ticket"
                  },
                  "message": {
                    "type": "string",
                    "description": "Content of the ticket"
                  },
                  "importance": {
                    "type": "string",
                    "description": "Importance level of the ticket",
                    "enum": [
                      "LOW",
                      "MEDIUM",
                      "HIGH"
                    ]
                  }
                },
                "required": [
                  "subject",
                  "message",
                  "importance"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Support Ticket created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          },
          "400": {
            "description": "Invalid request",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "401": {
            "description": "Unauthorized, admin permission required",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal server error",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "message": {
                      "type": "string",
                      "description": "Error message"
                    }
                  }
                }
              }
            }
          }
        },
        "security": [
          {
            "ApiKeyAuth": []
          }
        ]
      }
    },
    "/api/user/support/ticket/structure": {
      "get": {
        "summary": "Get form structure for support tickets",
        "operationId": "getSupportTicketsStructure",
        "tags": [
          "Support Tickets"
        ],
        "responses": {
          "200": {
            "description": "Form structure for support tickets",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "oneOf": [
                      {
                        "type": "object",
                        "properties": {
                          "type": {
                            "type": "string",
                            "enum": [
                              "input",
                              "select",
                              "switch",
                              "file"
                            ]
                          },
                          "label": {
                            "type": "string"
                          },
                          "name": {
                            "type": "string"
                          },
                          "placeholder": {
                            "type": "string",
                            "nullable": true
                          },
                          "options": {
                            "type": "array",
                            "items": {
                              "type": "string"
                            },
                            "nullable": true
                          },
                          "fileType": {
                            "type": "string",
                            "nullable": true
                          },
                          "width": {
                            "type": "integer",
                            "nullable": true
                          },
                          "height": {
                            "type": "integer",
                            "nullable": true
                          },
                          "maxSize": {
                            "type": "number",
                            "nullable": true
                          },
                          "notNull": {
                            "type": "boolean",
                            "nullable": true
                          },
                          "ts": {
                            "type": "string"
                          }
                        },
                        "required": [
                          "type",
                          "label",
                          "name"
                        ]
                      },
                      {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "type": {
                              "type": "string",
                              "enum": [
                                "input",
                                "select",
                                "switch",
                                "file"
                              ]
                            },
                            "label": {
                              "type": "string"
                            },
                            "name": {
                              "type": "string"
                            },
                            "placeholder": {
                              "type": "string",
                              "nullable": true
                            },
                            "options": {
                              "type": "array",
                              "items": {
                                "type": "string"
                              },
                              "nullable": true
                            },
                            "fileType": {
                              "type": "string",
                              "nullable": true
                            },
                            "width": {
                              "type": "integer",
                              "nullable": true
                            },
                            "height": {
                              "type": "integer",
                              "nullable": true
                            },
                            "maxSize": {
                              "type": "number",
                              "nullable": true
                            },
                            "notNull": {
                              "type": "boolean",
                              "nullable": true
                            },
                            "ts": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "type",
                            "label",
                            "name"
                          ]
                        }
                      }
                    ]
                  }
                }
              }
            }
          }
        },
        "security": []
      }
    }
  },
  "components": {
    "schemas": {},
    "responses": {},
    "parameters": {},
    "requestBodies": {},
    "securitySchemes": {
      "ApiKeyAuth": {
        "type": "apiKey",
        "in": "header",
        "name": "X-API-KEY"
      }
    }
  },
  "tags": []
}